---
title: "22. 도커(docker)"
nav_order: 28
layout: default
---

# 22. 도커 (docker)

## Docker란?

- 애플리케이션과 그 종속성을 **컨테이너**라는 경량 가상 환경에 패키징해 어디서나 일관되게 실행할 수 있도록 돕는 플랫폼  
- 개발·테스트·배포·운영 환경 간 차이를 최소화해 “로컬에서 잘 되던 코드가 서버에서 안 돼요” 문제를 방지  

## 사전 과제: 개인 로컬 PC에 Docker 설치

Day 5 Docker 실습은 개인 로컬 PC에서 진행하므로, 교육 전에 Docker를 설치하고 아래 명령어가 동작하는지 확인한다.

```bash
docker --version
docker run --rm hello-world
```

아래 실습 예시는 `docker` 명령을 기준으로 작성했다. 환경에 따라 Docker Desktop 또는 Docker Engine을 사용하면 된다.

환경별 설치 방법은 다음 중 하나를 선택한다.

| 환경 | 권장 설치 방법 |
| --- | --- |
| Windows | Docker Desktop 설치 ([공식 문서](https://docs.docker.com/desktop/setup/install/windows-install/)) 및 VS Code 통합 터미널 사용 |
| macOS | Docker Desktop 설치 ([공식 문서](https://docs.docker.com/desktop/setup/install/mac-install/)) |
| Ubuntu | Docker Engine 설치 ([공식 문서](https://docs.docker.com/engine/install/ubuntu/)) |

> 라이선스 주의: Docker Desktop은 개인 사용, 교육, 소규모 조직 등에는 무료로 사용할 수 있지만, Docker가 정한 규모를 넘는 기업의 상업적 사용에는 유료 구독이 필요할 수 있다. 회사 장비에서 설치하는 경우에는 기관의 소프트웨어 사용 정책과 [Docker Desktop 라이선스](https://docs.docker.com/subscription/desktop-license/)를 확인한다.

### macOS

1. Docker Desktop for Mac을 설치한다.
2. 설치 후 Docker Desktop을 실행한다.
3. 상단 메뉴바에 Docker 아이콘이 표시되고 실행 상태가 될 때까지 기다린다.
4. 터미널에서 아래 명령어를 실행한다.

```bash
docker --version
docker run --rm hello-world
```

Apple Silicon(M1/M2/M3) Mac과 Intel Mac은 설치 파일이 다를 수 있으므로 본인 장비에 맞는 버전을 선택한다.

### Windows

1. Docker Desktop for Windows를 설치한다.
2. 설치 과정에서 WSL 2 사용 안내가 나오면 안내에 따라 WSL 2를 활성화한다.
3. 설치 후 Docker Desktop을 실행한다.
4. VS Code를 설치하고, 하단의 통합 터미널에서 아래 명령어를 실행한다.

```powershell
docker --version
docker run --rm hello-world
```

Windows에서는 Docker Desktop이 실행 중이어야 `docker` 명령어가 정상 동작한다.

### 대체 선택지

Docker Desktop 사용이 부담되는 환경에서는 Linux 서버 기준으로 Docker Engine을 사용할 수 있다. 다만 교육 실습은 Docker Desktop 기준으로 진행한다.

| 환경 | 대체 선택지 | 비고 |
| --- | --- | --- |
| Ubuntu/Linux | Docker Engine | 서버 환경에서 가장 직접적인 설치 방식 |

## Docker의 주요 구성 요소

### 1. 이미지 (Image)
- 컨테이너를 생성하기 위한 **읽기 전용 템플릿**  
- 여러 계층(layer)으로 구성되며, 각 계층은 이전 계층 대비 변경 사항을 담음  
- **베이스 이미지**: 직접 개발자가 선택하는 최소 OS 또는 런타임 (예: `ubuntu`, `alpine`)  
- **커스텀 이미지**: 베이스 이미지 위에 애플리케이션·설정·라이브러리를 추가한 것  

### 2. 컨테이너 (Container)
- 이미지를 **실행한 인스턴스**로, 독립된 파일 시스템·프로세스 네임스페이스·네트워크 네임스페이스 등을 가짐  
- 상태 저장(pause/start/stop) 가능, 컨테이너 내부 변경은 이미지에 자동 반영되지 않음  

### 3. Dockerfile
- 이미지 빌드를 정의하는 **설정 파일**  
- `FROM`, `COPY`, `RUN`, `CMD`, `EXPOSE` 등 단계별 명령을 순차 실행  
- 각 단계가 캐시되어 변경된 부분만 다시 빌드하므로 효율적  

## Docker의 주요 기능

- 애플리케이션 격리
  - Docker는 컨테이너를 사용해 서로 다른 작업을 분리된 환경에서 실행한다.
- 효율적인 리소스 사용
  - 호스트 시스템의 커널을 공유하므로 가상 머신보다 가볍게 동작한다.
- 이식성
  - 이미지를 한 번 만들면 같은 조건의 환경에서 반복 실행하기 쉽다.
- 빠른 배포
  - 실행 환경을 이미지로 묶어 두므로 시작과 재현이 빠르다.

## Docker의 동작 방식

1. 이미지 빌드
    - Dockerfile을 읽어서 이미지를 만든다.

    ```bash
    docker build -t myapp .
    ```
2. 컨테이너 실행
    - 이미지로부터 컨테이너를 생성하고 실행한다.

    ```bash
    docker run -d -p 8080:80 myapp
    ```
3. 컨테이너 관리
    - 실행 중인 컨테이너를 확인하고 멈추거나 다시 시작할 수 있다.

    ```bash
    docker ps
    docker stop myapp
    docker start myapp
    docker logs myapp
    ```

## Dockerfile 빌드 및 실행 방법

1. Docker가 실행 중인지 확인한다.
2. Dockerfile이 있는 디렉터리에서 이미지를 빌드한다.
3. 빌드한 이미지를 실행한다.

```bash
cd ~/myapp
docker build -t myapp:latest .
docker run -d -p 5000:5000 myapp:latest
```

Docker Desktop과 Docker Engine처럼 환경이 달라도 기본 흐름은 같다.

## 프로세스 vs 도커 컨테이너

### 도커 컨테이너는 프로세스와 유사하다

- 도커 컨테이너는 실제로 하나 이상의 프로세스를 실행하는 격리된 환경이다.
- 각 컨테이너는 독립된 네임스페이스와 리소스를 사용하여 격리된 상태에서 실행된다.
- 도커는 CPU, 메모리, I/O 등의 자원을 관리하고 할당한다.
- 자원 제한이나 우선 순위는 사용자가 설정한 도커 설정에 따라 결정된다.
- 예를 들어, docker run 명령어에서 --memory나 --cpus 옵션을 사용하여 자원을 제한할 수 있다.

### Docker 컨테이너 자원 제한

여러 사용자가 함께 쓰는 서버에서는 컨테이너가 호스트의 CPU와 메모리를 과도하게 사용하지 않도록 제한하는 것이 좋다.

```bash
# CPU 2개, 메모리 4GB까지 사용하도록 제한
docker run --rm --cpus=2 --memory=4g ubuntu:22.04 bash

# 특정 CPU 코어만 사용하도록 제한
docker run --rm --cpuset-cpus="0,1" --memory=2g ubuntu:22.04 bash

# 실행 중인 컨테이너의 자원 사용량 확인
docker stats
```

바이오 데이터 분석 작업은 큰 파일을 읽고 쓰는 경우가 많으므로 CPU뿐 아니라 메모리와 디스크 사용량도 함께 확인해야 한다.

### 도커 이미지는 스크립트와 유사하다

- 도커 이미지는 컨테이너를 실행하기 위한 모든 필요한 파일과 설정을 포함한 패키지이다.
- 이는 실행 가능한 명령어들의 모음인 스크립트와 유사하다.

### 도커 이미지는 도커의 규칙과 표준에 따라 만들어진다.

- Dockerfile을 사용하여 이미지를 정의하고, docker build 명령어를 사용하여 이미지를 생성한다.
- 이미지는 종속성과 애플리케이션 코드를 포함하여 일관된 환경을 제공한다.

### docker run은 스크립트를 실행하는 것과 유사하다.

- docker run 명령어는 도커 이미지를 기반으로 새로운 컨테이너를 생성하고, 이를 실행한다. 이는 스크립트를 실행하여 명령어들을 수행하는 것과 유사하다.
- docker run 명령어는 이미지에서 지정한 CMD나 ENTRYPOINT를 실행한다.

- [[번외] 프로세스와 도커 컨테이너](extra/process.md)

## [실습] 도커 이미지 만들기 (로컬 PC에서 실행)

- 도커가 없을 경우, 사전 과제의 설치 안내를 먼저 따라간다.

    ```bash
    mkdir -p ~/docker
    cd ~/docker
    ```


- `echo_docker.sh` 파일 작성
```bash
#!/bin/sh
echo "Hello, Docker!"
```

```bash
chmod +x echo_docker.sh
```

```dockerfile
FROM alpine:latest

WORKDIR /app

COPY echo_docker.sh .
RUN chmod +x echo_docker.sh

CMD ["./echo_docker.sh"]
```

- `Dockerfile` 파일 생성
    - Alpine Linux 기반 컨테이너를 만들고
    - /app 디렉터리에 로컬 스크립트를 복사한 뒤
    - 실행 권한을 주고
    - 컨테이너가 시작되면 그 스크립트를 실행하도록 설정한다.


- 이미지 빌드
    ```bash
    docker build --no-cache -t my-echo-app:latest .
    ```

- 이미지 확인

    ```bash
    docker images
    ```

- 이미지 실행

    ```bash
    docker run --rm my-echo-app
    ```
    - docker
        - Docker CLI(커맨드라인 인터페이스)를 호출한다는 뜻.
    - run
        - 새 컨테이너 생성 후 실행” 하라는 서브커맨드
        - 내부적으로는 docker create + docker start를 한 번에 처리한다.
    - --rm
        – 컨테이너가 종료되면 자동으로 해당 컨테이너 인스턴스를 삭제(remove)하라는 옵션.
        – 로그·파일 등이 남지 않아 일회성 테스트용으로 좋다.
    - my-echo-app
        – 실행할 이미지 이름.
        – docker build -t my-echo-app . 처럼 미리 빌드해 둔 이미지를 가리킨다.
        – 이 이미지에 설정된 기본 커맨드(예: ENTRYPOINT나 CMD)가 실행된다.

- 사용하지 않는 이미지 삭제
    ```bash
    docker rmi <id>
    ```

## 바이오 분석에서 Docker 실행 방식

바이오 데이터 분석에서는 Docker를 웹 서비스처럼 계속 실행하기보다, 입력 데이터를 받아 분석을 수행하고 결과 파일을 남긴 뒤 종료되는 배치성 파이프라인으로 사용하는 경우가 많다.

이 방식은 호스트의 입력/출력 디렉터리를 컨테이너에 볼륨 마운트하고, 작업 종료 후 컨테이너를 자동 삭제하는 `--rm` 구조와 잘 맞는다.

일반적인 흐름은 다음과 같다.

1. 호스트 서버에 입력 데이터 디렉터리를 준비한다.
2. Docker 컨테이너를 실행하면서 입력/출력 디렉터리를 볼륨 마운트한다.
3. 컨테이너 내부에서 분석 스크립트가 실행된다.
4. 결과 파일은 호스트의 출력 디렉터리에 저장된다.
5. 컨테이너는 작업이 끝나면 종료되고 `--rm` 옵션으로 자동 삭제된다.

## [실습] Docker 배치 파이프라인

이 실습에서는 실제 유전체 데이터나 전문 바이오 분석 툴을 사용하지 않는다. 임의의 문자열이 많이 들어 있는 텍스트 파일을 가상의 분석 데이터로 보고, 컨테이너 안에서 `grep`, `wc`, `awk` 같은 리눅스 기본 명령어를 실행한다.

- [[실습] Docker 배치 파이프라인 - 30분](training/batch_pipeline.md)

실제 바이오 분석 환경에서는 이 구조를 직접 `docker run`으로 실행하기도 하지만, 기관이나 서버 환경에 따라 Nextflow, Snakemake 같은 워크플로 도구나 Apptainer/Singularity 같은 HPC 친화적인 컨테이너 도구를 통해 실행하기도 한다.

## 로컬에서 만든 Docker 작업을 서버에서 실행하기

이번 실습에서는 개인 로컬 PC에서 `Dockerfile`, 실행 스크립트, 설정 파일을 먼저 작성한 뒤, `scp`로 분석 서버에 전송하고 서버에서 이미지를 빌드해 실행하는 흐름을 연습한다.

실제 현장에서는 기관 환경에 따라 방식이 다를 수 있다. Docker Hub, GitHub Container Registry 같은 이미지 저장소를 사용하거나, Nextflow/Snakemake 같은 워크플로 도구가 컨테이너 실행을 대신 관리하기도 한다. HPC 환경에서는 Docker 대신 Apptainer/Singularity를 사용하는 경우도 많다.

여기서는 복잡한 배포 체계 대신, 분석 코드와 Docker 설정을 서버로 옮기고 서버에 있는 데이터 디렉터리를 마운트해 실행하는 기본 구조만 다룬다.

### 1. 로컬 작업 디렉터리 정리

로컬 PC에서 다음 파일이 준비되어 있다고 가정한다.

```text
docker_batch/
├── Dockerfile
├── run_pipeline.sh
└── input/
    └── mock_data.txt
```

실제 서버 분석에서는 `input/` 아래에 작은 테스트 파일만 같이 보내고, 큰 원본 데이터는 서버의 별도 경로를 마운트해서 사용하는 편이 좋다.

### 2. scp로 서버에 전송

로컬 PC에서 실행한다.

```bash
scp -r ~/docker_batch username@server_address:~/docker_batch
```

서버 SSH 포트가 기본값 22가 아니라면 `-P` 옵션을 사용한다.

```bash
scp -P 1119 -r ~/docker_batch username@server_address:~/docker_batch
```

### 3. 서버에서 이미지 빌드

서버에 SSH로 접속한 뒤 실행한다.

```bash
ssh username@server_address
cd ~/docker_batch
docker build -t bio-batch-demo:latest .
```

이미지 목록을 확인한다.

```bash
docker images
```

### 4. 서버 데이터 디렉터리를 마운트해서 실행

서버에 실제 분석 데이터가 `/data/project/input`에 있고 결과를 `/data/project/output`에 남긴다고 가정한다.

```bash
mkdir -p /data/project/output

docker run --rm \
  --cpus=4 \
  --memory=8g \
  -v /data/project/input:/data/input:ro \
  -v /data/project/output:/data/output \
  bio-batch-demo:latest
```

작업이 끝나면 결과 파일만 서버의 출력 디렉터리에 남는다.

```bash
ls -lh /data/project/output
```

## Docker 컨테이너 vs. Conda 가상환경

| 구분          | Docker 컨테이너                             | Conda 가상환경                      |
| ----------- | --------------------------------------- | ------------------------------- |
| **격리 범위**   | OS 수준: 프로세스 격리, 파일시스템 격리, 네트워크 네임스페이스 등 | 언어/패키지 수준: Python 등 런타임 패키지만 격리 |
| **커널 사용**   | 호스트 커널 공유                               | 호스트 OS에 종속                      |
| **재현성**     | OS부터 애플리케이션까지 그대로 패키징                   | 파이썬 패키지 버전·의존성만 고정              |
| **용량·오버헤드** | 비교적 무거움(수십\~백 MB)                       | 가볍다(수십 MB 미만)                   |
| **주 사용처**   | 서비스 배포·마이크로서비스·CI/CD·테스트                | 개발 환경 분리·데이터 과학 프로젝트            |

- 도커 주의 사항 (용량)
    - `docker images` 에서 용량 확인
    - 이미지는 주기적으로 정리해 저장 공간을 관리한다.
