---
title: "24. 병렬처리 (SLURM)"
nav_order: 30
layout: default
---

# 24. 병렬처리 (SLURM)

## SLURM 소개

SLURM(Scheduler for Large-scale Resource Management)은 오픈 소스 클러스터 자원 관리 및 작업 스케줄링 시스템이다.
대규모 HPC(High Performance Computing) 환경에서 병렬 작업을 실행할 때 주로 사용한다.
작업 큐, 우선순위, 노드 상태 등을 관리해 여러 사용자의 작업을 효율적으로 배분한다.

## 주요 개념

### 컨트롤 노드와 워커 노드

SLURM은 여러 서버를 하나의 계산 자원처럼 묶어서 사용하게 해준다.
이때 모든 서버가 같은 역할을 하는 것은 아니다.

| 구성 요소 | 역할 |
| --- | --- |
| 컨트롤 노드(Control node) | 작업 큐, 노드 상태, 자원 배정, 작업 스케줄링을 관리한다. |
| 워커 노드(Worker node) | 컨트롤 노드가 배정한 실제 계산 작업을 실행한다. |
| 사용자 | `sbatch`, `srun` 같은 명령으로 작업을 제출한다. |

일반적인 흐름은 다음과 같다.

1. 사용자가 컨트롤 노드에 작업을 제출한다.
2. 컨트롤 노드가 현재 비어 있는 워커 노드와 자원을 확인한다.
3. 컨트롤 노드가 적절한 워커 노드에 작업 실행을 지시한다.
4. 워커 노드가 실제 명령어를 실행한다.
5. 실행 결과는 지정한 출력 파일이나 공유 파일 시스템에 저장된다.

SLURM 데몬 이름으로 보면 컨트롤 노드에서는 `slurmctld`가 동작하고, 워커 노드에서는 `slurmd`가 동작한다.
단일 노드 실습 환경에서는 한 서버가 컨트롤 노드이면서 동시에 워커 노드 역할을 한다.

### Munge 인증

SLURM 클러스터에서는 컨트롤 노드와 워커 노드가 서로를 신뢰할 수 있어야 한다.
이때 주로 사용하는 인증 방식이 Munge이다.

Munge는 노드 사이에서 주고받는 작업 요청이 신뢰할 수 있는 노드와 사용자에게서 온 것인지 확인한다.
예를 들어 컨트롤 노드가 워커 노드에 작업 실행을 지시할 때, 워커 노드는 Munge 인증을 통해 해당 요청이 같은 클러스터에서 온 정상 요청인지 확인한다.

여러 노드로 구성된 실제 클러스터에서는 모든 노드가 같은 `/etc/munge/munge.key`를 사용해야 한다.
키가 서로 다르면 컨트롤 노드와 워커 노드가 서로를 인증하지 못해 작업 제출이나 실행이 실패할 수 있다.

### 노드(Node)와 파티션(Partition)

**노드**는 실제 작업을 실행하는 서버 또는 컴퓨팅 유닛이다.
**파티션**은 노드를 논리적으로 묶은 그룹이다. 예를 들어 GPU 파티션이나 CPU 전용 파티션으로 나눌 수 있다.

### 작업(Job)과 배치 스크립트

**작업(Job)**은 SLURM에 제출되는 실행 단위다.
**배치 스크립트**는 실행 명령어와 자원 요청 정보를 담은 셸 스크립트다.


## SLURM 설치

아래 예시는 단일 노드 실습 환경을 기준으로 한 간단한 구성이다. 실제 클러스터에서는 컨트롤 노드와 워커 노드 설정을 더 세밀하게 분리해야 한다.

```bash
sudo apt update
sudo apt install -y slurm-wlm munge
```

## Munge 설정

아래 명령어는 단일 노드 실습 환경에서 Munge key를 새로 만드는 예시다.
실제 여러 노드 클러스터에서는 컨트롤 노드에서 만든 `/etc/munge/munge.key`를 모든 워커 노드에 동일하게 복사해야 한다.

```bash
# Munge key 생성
sudo dd if=/dev/urandom bs=1 count=1024 | sudo tee /etc/munge/munge.key > /dev/null
sudo chown -R munge:munge /etc/munge
sudo chmod 0700 /etc/munge
sudo chmod 400 /etc/munge/munge.key

# 로그 디렉터리 생성
sudo mkdir -p /var/log/munge
sudo chown munge:munge /var/log/munge

# munge 서비스 시작
sudo systemctl enable --now munge
```

여러 노드 클러스터에서는 각 노드에서 `munge` 서비스가 실행 중이어야 하며, Munge key의 소유자와 권한도 동일하게 맞춰야 한다.
단일 노드 실습에서는 같은 서버 안에서 `slurmctld`와 `slurmd`가 통신하므로 위 설정만으로 구조를 확인할 수 있다.

## SLURM 디렉터리 준비

```bash
sudo mkdir -p /var/spool/slurmd
sudo mkdir -p /var/spool/slurmctld
sudo mkdir -p /var/log/slurm

sudo chown -R slurm:slurm /var/spool/slurmd
sudo chown -R slurm:slurm /var/spool/slurmctld
sudo chown -R slurm:slurm /var/log/slurm
```

## SLURM 설정 예시 (`/etc/slurm/slurm.conf`)

먼저 현재 서버의 호스트 이름과 CPU 개수를 확인한다.

```bash
hostname -s
nproc
```

아래 설정에서 `{호스트이름}`은 `hostname -s` 결과로, `CPUs=2`는 `nproc` 결과에 맞게 수정한다.

```conf
ClusterName=single-cluster
ControlMachine={호스트이름}

AccountingStorageType=accounting_storage/none
JobAcctGatherType=jobacct_gather/none

NodeName={호스트이름} CPUs=2 State=UNKNOWN
PartitionName=debug Nodes={호스트이름} Default=YES MaxTime=INFINITE State=UP
```


## SLURM 데몬 실행

```bash
# 컨트롤 노드에서 실행한다. 단일 노드 환경에서는 같은 서버에서 모두 실행한다.
sudo systemctl enable --now slurmctld

# 워커 노드에서 실행한다.
sudo systemctl enable --now slurmd
```

`slurmctld`는 작업을 어느 노드에서 실행할지 결정하는 스케줄러 역할을 하고, `slurmd`는 각 워커 노드에서 실제 작업 실행을 담당한다.
단일 노드 실습에서는 두 데몬을 같은 서버에서 실행하지만, 실제 클러스터에서는 보통 컨트롤 노드와 여러 워커 노드로 역할이 나뉜다.

## SLURM 기본 명령어

| 명령어         | 설명                  |
| ----------- | ------------------- |
| `sinfo`     | 노드 및 파티션 상태 확인      |
| `squeue`    | 실행 중인 작업 목록 확인      |
| `squeue -u` | 특정 사용자 작업 확인        |
| `sbatch`    | 배치 스크립트 제출          |
| `srun`      | 직접 명령 실행 (인터랙티브 실행) |
| `scancel`   | 작업 취소               |


## SLURM 배치 스크립트 예시

### `myjob.sh`

```bash
#!/bin/bash
#SBATCH --job-name=test_job
#SBATCH --output=output.txt
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=2
#SBATCH --mem=4G
#SBATCH --time=00:05:00
#SBATCH --partition=debug

echo "Hello from SLURM"
echo "CPUs per task: $SLURM_CPUS_PER_TASK"
hostname
```

### 실행 및 확인

```bash
sbatch myjob.sh
cat output.txt
```


## SLURM 자원 요청 옵션 요약

| 옵션                   | 설명              | 예시                    |
| -------------------- | --------------- | --------------------- |
| `--job-name=이름`      | 작업 이름 지정        | `--job-name=myjob`    |
| `--output=파일명`       | 표준 출력 파일 지정     | `--output=result.txt` |
| `--ntasks=숫자`        | 실행할 태스크 개수      | `--ntasks=4`          |
| `--cpus-per-task=숫자` | 태스크당 할당할 CPU 개수 | `--cpus-per-task=2`   |
| `--mem=용량`           | 작업 전체에 할당할 메모리 | `--mem=8G`            |
| `--mem-per-cpu=용량`   | CPU 1개당 할당할 메모리 | `--mem-per-cpu=2G`    |
| `--time=HH:MM:SS`    | 최대 실행 시간        | `--time=01:00:00`     |
| `--partition=이름`     | 사용할 파티션 이름      | `--partition=short`   |

CPU 개수만 많이 요청한다고 항상 작업이 빨라지는 것은 아니다. 프로그램이 멀티스레드를 지원해야 `--cpus-per-task` 값을 활용할 수 있으며, 메모리가 부족하면 작업이 느려지거나 실패할 수 있다.


## SLURM 상태 확인 및 관리

```bash
# 현재 노드 상태
sinfo

# 현재 큐 상태
squeue

# 특정 사용자 작업 확인
squeue -u 사용자명

# 작업 취소
scancel <JOB_ID>
```
