---
title: "24. 병렬처리 (SLURM)"
nav_order: 30
layout: default
---

# 24. 병렬처리 (SLURM)

## SLURM 소개

- SLURM(Scheduler for Large-scale Resource Management)은 오픈 소스 클러스터 자원 관리 및 작업 스케줄링 시스템
- 대규모 HPC(High Performance Computing) 환경에서 병렬 작업 실행에 사용
- 작업 큐, 우선순위, 노드 상태 등을 제어하여 효율적인 병렬 실행을 지원

## 주요 개념

### 노드(Node)와 파티션(Partition)

- **노드**: 실제 작업을 실행하는 서버 또는 컴퓨팅 유닛
- **파티션**: 노드를 논리적으로 묶은 그룹 (예: GPU 파티션, CPU 전용 파티션)

### 작업(Job)과 배치 스크립트

- **작업(Job)**: SLURM에 제출되는 실행 단위
- **배치 스크립트**: 실행 명령어 및 자원 요청 정보를 담은 셸 스크립트


## SLURM 설치

```bash
sudo apt update
sudo apt install slurm-wlm munge
````

## Munge 설정

```bash
# Munge key 생성
sudo dd if=/dev/urandom bs=1 count=1024 | sudo tee /etc/munge/munge.key > /dev/null
sudo chown -R munge:munge /etc/munge
sudo chmod 0700 /etc/munge
sudo chmod 400 /etc/munge/munge.key

# 로그 디렉토리 생성
sudo mkdir -p /var/log/munge
sudo chown munge:munge /var/log/munge

# munge 서비스 시작
sudo systemctl enable --now munge
```

## SLURM 디렉토리 준비

```bash
sudo mkdir -p /var/spool/slurmd
sudo mkdir -p /var/spool/slurmctld
sudo mkdir -p /var/log/slurm

sudo chown slurm: /var/spool
sudo chown slurm: /var/spool/slurmd
sudo chown slurm: /var/spool/slurmctld
sudo chown slurm: /var/log/slurm
```

## SLURM 설정 예시 (`/etc/slurm/slurm.conf`)

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
# 마스터 노드에서 실행 (단일 노드 환경에서는 둘 다 실행)
sudo systemctl enable --now slurmctld

# 워커 노드에서 실행
sudo systemctl enable --now slurmd
```


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
#SBATCH --time=00:05:00
#SBATCH --partition=debug

echo "Hello from SLURM"
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
| `--time=HH:MM:SS`    | 최대 실행 시간        | `--time=01:00:00`     |
| `--partition=이름`     | 사용할 파티션 이름      | `--partition=short`   |


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