---
title: "18. 패키지 관리 및 가상 환경 - Conda (Miniconda 기반)"
nav_order: 24
layout: default
---

# 18. 패키지 관리 및 가상 환경 - Conda (Miniconda 기반)

## Conda 소개

Conda는 오픈 소스 패키지 및 가상 환경 관리 도구다.
Python, R, Ruby 등 다양한 언어를 지원하며, 데이터 과학과 머신러닝, 소프트웨어 개발 환경에서 널리 사용된다.

## 주요 기능

### 패키지 관리

패키지를 설치, 업데이트, 제거할 수 있으며, 의존성도 함께 관리한다.

### 가상 환경 관리

프로젝트별로 독립된 환경을 만들 수 있어, 서로 다른 프로젝트 간 충돌을 줄일 수 있다.


## 가상화 및 가상 환경의 차이

### 가상화 (Virtualization)

물리 하드웨어를 여러 개의 VM으로 나누는 방식이다.
주요 도구로는 VirtualBox, VMware, UTM 등이 있다.

### 가상 환경 (Virtual Environment)

OS 내부에서 프로젝트별로 독립된 실행 환경을 만드는 방식이다.
주요 도구로는 conda, venv, virtualenv가 있다.


## Miniconda 소개

Miniconda는 Conda와 Python만 포함한 가장 가벼운 설치 버전이다.
필요한 패키지만 직접 선택해서 설치할 수 있어, 교육용이나 기본 환경 구성용으로 적합하다.

## Miniconda 설치

### 1. 다운로드

```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

- Apple Silicon 환경
```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh
```

### 2. 설치 실행

```bash
$ bash Miniconda3-latest-Linux-x86_64.sh
```

* 라이선스 동의 필요 ("yes")

### 3. 환경 변수 등록

```bash
$ echo 'eval "$(~/miniconda3/bin/conda shell.bash hook)"' >> ~/.bashrc
$ source ~/.bashrc
```

### 4. 설치 확인

```bash
$ conda --version
```


## 가상 환경 생성 및 사용

### 1. YAML 환경 정의 파일

`environment.yml` 파일을 아래와 같이 작성

```yaml
name: myenv
channels:
  - conda-forge
dependencies:
  - figlet
variables:
  VALUE1: "hello"
```

### 2. 환경 생성

```bash
$ conda env create -f environment.yml
```

### 3. 환경 활성화

```bash
$ conda activate myenv
$ echo $VALUE1  # hello
$ figlet CONDA
```

### 4. 환경 비활성화

```bash
$ conda deactivate
```


## Conda 환경 변수 확인

### 1. 외부 환경 변수 등록

```bash
$ export VALUE1=external_value1
$ export VALUE2=external_value2
$ echo $VALUE1
$ echo $VALUE2
```

### 2. 설치한 Conda 환경 활성화

```bash
$ conda activate myenv
$ echo $VALUE1
$ echo $VALUE2
```

### 3. Conda 비활성화

```bash
$ conda deactivate
$ echo $VALUE1
$ echo $VALUE2
```

## Conda 활성화/비활성화 시 실행되는 스크립트

### 1. 실행 전 환경 변수 등록

```bash
$ export SCRIPT_VALUE="init"
```

### 2. 활성화 시 실행되는 스크립트 등록

```bash
$ mkdir -p ~/miniconda3/envs/myenv/etc/conda/activate.d
$ echo 'export SCRIPT_VALUE="after_active"' > ~/miniconda3/envs/myenv/etc/conda/activate.d/env_vars.sh
$ chmod +x ~/miniconda3/envs/myenv/etc/conda/activate.d/env_vars.sh
```

### 3. 비활성화 시 실행되는 스크립트 등록

```bash
$ mkdir -p ~/miniconda3/envs/myenv/etc/conda/deactivate.d
$ echo 'export SCRIPT_VALUE="after_deactive"' > ~/miniconda3/envs/myenv/etc/conda/deactivate.d/env_vars.sh
$ chmod +x ~/miniconda3/envs/myenv/etc/conda/deactivate.d/env_vars.sh
```

[[실습] Conda 환경별 변수 확인 - 15분](training/conda_env_variable.md)


## Conda vs Miniconda vs Anaconda

| 항목     | Conda     | Miniconda      | Anaconda                 |
| ------ | --------- | -------------- | ------------------------ |
| 구성 요소  | 패키지 관리 도구 | Conda + Python | Miniconda + 과학 패키지 1500+ |
| 설치 여부  | 별도 설치 필요      | 가볍게 설치 가능         | 무겁고 전체 포함                |
| 사용 자유도 | 높음        | 높음             | 낮음                       |
| 권장 용도  | 고급 개발자 선택 | 개발, 교육용        | 데이터 과학 입문/분석용            |


## [[번외] 아나콘다](extra/anaconda.md)
