---
title: "18. 패키지 관리 및 가상 환경 - Conda (Miniconda 기반)"
nav_order: 24
layout: default
---

# 18. 패키지 관리 및 가상 환경 - Conda (Miniconda 기반)

## Conda 소개

* Conda는 오픈 소스 패키지 및 가상 환경 관리 도구
* Python, R, Ruby 등 다양한 언어 지원
* 데이터 과학, 머신런리닝, 소프트웨어 개발 등에서 활용

## 주요 기능

### 패키지 관리

* 다양한 패키지 설치, 업데이트, 제거 가능
* 의언성 자동 해결

### 가상 환경 관리

* 프로젝트별 동반 환경 생성
* 환경과 환경 간 충돌 방지


## 가상화 및 가상 환경의 차이

### 가상화 (Virtualization)

* 무리 패스 하드웨어를 VM으로 분리
* 주요 도구: VirtualBox, VMware, UTM 등

### 가상 환경 (Virtual Environment)

* OS 내부에서 프로젝트별 동반한 환경 구성
* 주요 도구: conda, venv, virtualenv


## Miniconda 소개

* Conda + Python 까지만 포함한 가장 가병한 설치 버전
* 필요한 패키지만 선택 설치 가능
* 가볍게 설치 가능, 라이센스 제약 적용 적적

## Miniconda 설치

### 1. 다운로드

```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

- Apple Silicon Server
```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh
```

### 2. 설치 시험

```bash
$ bash Miniconda3-latest-Linux-x86_64.sh
```

* 라이센스 동의 필요 ("yes")

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
  - defaults
dependencies:
  - python=3.9
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
```

### 4. 환경 비활성화

```bash
$ conda deactivate
```


## Conda 패키지 가이드

### 1. Conda 가상 환경 변수 등록

```bash
$ export VALUE1=external_value1
$ export VALUE2=external_value2
$ echo $VALUE1
$ echo $VALUE2
```

### 2. Python 설치 및 버전 확인

```bash
$ sudo apt install python3
$ python3 --version
```

### 3. 설치한 Conda 환경 활성화

```bash
$ conda activate myenv
$ echo $VALUE1
$ echo $VALUE2
$ python3 --version
```

### 4. Conda 비활성화

```bash
$ conda deactivate
$ echo $VALUE1
$ echo $VALUE2
$ python3 --version
```

## Conda 활성화/비활성화 시 실행되는 스크립트

### 1. 실작 전 환경 변수 등록

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


## Conda vs Miniconda vs Anaconda

| 항목     | Conda     | Miniconda      | Anaconda                 |
| ------ | --------- | -------------- | ------------------------ |
| 구성 요소  | 패키지 관리 도구 | Conda + Python | Miniconda + 과학 패키지 1500+ |
| 설치 여부  | 규칙없음      | 가볍고 가능         | 무겁고 전체 포함                |
| 자용 자유도 | 높음        | 높음             | 낮음                       |
| 권장 용도  | 고급 개발자 선택 | 개발, 교육용        | 데이터 과학 입문/분석용            |


## [[번외] 아나콘다](extra/anaconda.md)
