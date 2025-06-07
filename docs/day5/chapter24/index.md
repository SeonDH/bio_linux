# 24. 병렬처리 (SLURM)

## SLURM 소개

- SLURM(Scheduler for Large-scale Resource Management)은 오픈 소스 클러스터 자원 관리 및 작업 스케줄링 시스템
- 대규모 HPC(High Performance Computing) 환경에서 병렬 작업 실행에 사용
- SLURM은 작업 큐, 우선순위, 노드 상태 등을 제어하여 효율적인 병렬 실행을 지원

## 주요 개념

### 노드(Node)와 파티션(Partition)

- **노드**: 실제 작업을 실행하는 서버 또는 컴퓨팅 유닛
- **파티션**: 노드를 논리적으로 묶은 그룹 (예: GPU 파티션, CPU 전용 파티션)

### 작업(Job)과 배치 스크립트

- **작업(Job)**: SLURM에 제출되는 실행 단위
- **배치 스크립트**: 실행 명령어 및 자원 요청 정보를 담은 셸 스크립트

## SLURM 설치 (로컬 테스트용)

```bash
sudo apt update
sudo apt install slurm-wlm
````

> 실제 HPC 환경에서는 별도 구성 파일(slurm.conf) 작성 및 MUNGE 인증 설정이 필요

## 기본 SLURM 명령어

| 명령어       | 설명                   |
| --------- | -------------------- |
| `sinfo`   | 노드 및 파티션 상태 확인       |
| `squeue`  | 현재 실행 중인 작업 목록 확인    |
| `sbatch`  | 작업 배치 스크립트 제출        |
| `scancel` | 작업 취소                |
| `srun`    | 명령을 직접 실행 (인터랙티브 실행) |

## SLURM 배치 스크립트 예시

```bash
#!/bin/bash
#SBATCH --job-name=test_job
#SBATCH --output=output.txt
#SBATCH --ntasks=1
#SBATCH --time=00:05:00
#SBATCH --partition=short

echo "Hello from SLURM"
hostname
```

### 실행 방법

```bash
sbatch myjob.sh
```

### 출력 확인

```bash
cat output.txt
```

## 병렬 작업 예시

### CPU 코어 4개 사용

```bash
#!/bin/bash
#SBATCH --job-name=multi_cpu
#SBATCH --ntasks=4
#SBATCH --time=00:10:00

srun hostname
```

### MPI 프로그램 실행 예시

```bash
#!/bin/bash
#SBATCH --ntasks=4

mpirun ./my_mpi_program
```

> `mpirun` 사용을 위해 OpenMPI 또는 MPICH 설치 필요

## SLURM 상태 확인 및 관리

```bash
# 현재 노드 상태 확인
sinfo

# 현재 큐에 있는 작업 확인
squeue

# 사용자 별 작업 확인
squeue -u 사용자명

# 특정 작업 취소
scancel <JOB_ID>
```

## SLURM 자원 요청 옵션 요약

| 옵션                   | 설명          |
| -------------------- | ----------- |
| `--job-name=이름`      | 작업 이름 지정    |
| `--output=파일`        | 표준 출력 파일 지정 |
| `--ntasks=숫자`        | 실행할 태스크 개수  |
| `--cpus-per-task=숫자` | 태스크당 CPU 수  |
| `--time=HH:MM:SS`    | 최대 실행 시간    |
| `--partition=이름`     | 사용할 파티션 지정  |
