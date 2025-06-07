---
title: "22. 도커(docker)"
nav_order: 28
layout: default
---

# 22. 도커 (docker)

## Docker란?

- 애플리케이션을 컨테이너라는 가상화된 환경에서 실행할 수 있게 해주는 플랫폼이다.
- 컨테이너는 애플리케이션과 그 종속성을 함께 패키징하여 어디서든 일관되게 실행할 수 있는 경량의 독립형 실행 환경이다.
- Docker는 개발, 테스트, 배포 및 운영 환경에서 일관성을 유지하면서 소프트웨어를 실행하는 데 도움을 준다.

## Docker의 주요 구성 요소

### 1. 이미지 (Image)

- 이미지는 컨테이너를 생성하기 위한 읽기 전용 템플릿이다.
- 애플리케이션 코드, 라이브러리, 종속성 등을 포함한다. 이미지는 여러 계층으로 구성되어 있으며, 각 계층은 이전 계층에 대한 변경 사항을 포함한다.
    - **베이스 이미지**: 다른 이미지를 기반으로 하지 않는 이미지이다. 예: `ubuntu`, `alpine`
    - **커스텀 이미지**: 베이스 이미지를 기반으로 사용자가 추가적으로 설정한 이미지이다.

### 2. 컨테이너 (Container)

- 컨테이너는 이미지를 실행한 인스턴스이다.
- 격리된 환경에서 애플리케이션을 실행할 수 있다.
- 컨테이너는 동일한 호스트 시스템에서 실행되지만, 각 컨테이너는 독립된 파일 시스템과 리소스를 사용한다.
- **상태**: 컨테이너는 상태를 가지며, 일시 정지, 시작, 중지, 재시작할 수 있다.
- **변경 사항**: 컨테이너에서 발생한 변경 사항은 이미지에 반영되지 않는다. 변경 사항을 반영하려면 새로운 이미지를 생성해야 한다.

### 3. Dockerfile

- Dockerfile은 이미지를 빌드하기 위한 설정 파일이다.
- 명령어의 집합으로 구성되어 있으며, 이를 통해 이미지를 빌드한다.
- Dockerfile은 단계별로 이미지를 빌드하며, 각 단계는 캐시되어 빌드 시간을 단축할 수 있다.
- **명령어**: `FROM`, `COPY`, `RUN`, `CMD`, `EXPOSE` 등이 있다.

# Docker의 주요 기능

### 1. 애플리케이션 격리

Docker는 컨테이너를 사용하여 애플리케이션을 격리된 환경에서 실행한다. 이는 다른 애플리케이션과의 충돌을 방지하고, 일관된 실행 환경을 제공한다.

### 2. 효율적인 리소스 사용

Docker는 호스트 시스템의 커널을 공유하여 가상 머신보다 더 효율적으로 리소스를 사용한다. 이는 컨테이너의 빠른 시작과 적은 오버헤드를 가능하게 한다.

### 3. 이식성

Docker 이미지는 한 번 빌드하면 어디서나 실행할 수 있다. 이는 개발, 테스트, 운영 환경 간의 일관성을 유지하는 데 도움을 준다.

### 4. 빠른 배포

Docker는 애플리케이션을 패키징하고 배포하는 과정을 단순화한다. 컨테이너는 빠르게 시작되고, 애플리케이션의 배포 시간을 단축할 수 있다.

# Docker의 동작 방식

### 1. 이미지 빌드

사용자는 Dockerfile을 작성하여 이미지를 빌드한다. Docker는 Dockerfile을 읽고, 명령어를 순차적으로 실행하여 이미지를 생성한다.

```
docker build -t myapp .
```

### 2. 컨테이너 실행

이미지로부터 컨테이너를 생성하고 실행한다. 사용자는 필요한 설정을 지정하여 컨테이너를 실행할 수 있다.

```
sudo docker run -d -p 8080:80 myapp
```

### 3. 컨테이너 관리

사용자는 실행 중인 컨테이너를 관리할 수 있다. 컨테이너를 일시 정지, 중지, 재시작할 수 있으며, 로그를 확인할 수 있다.

```
sudo docker ps            # 실행 중인 컨테이너 목록 보기
sudo docker stop myapp    # 컨테이너 중지
sudo docker start myapp   # 컨테이너 시작
sudo docker logs myapp    # 컨테이너 로그 보기
```

# Dockerfile 빌드 및 실행 방법

### 1. Docker 설치

리눅스 배포판(Ubuntu)에서 Docker를 설치하는 방법은 다음과 같다:

```
sudo apt-get update
sudo apt-get install -y docker.io
```

Docker 설치가 완료되면 Docker 데몬을 시작하고, 부팅 시 자동으로 시작되도록 설정한다:

```
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Dockerfile 빌드

Dockerfile이 있는 디렉토리로 이동하여 이미지를 빌드한다. `-t` 옵션을 사용하여 이미지를 태그할 수 있다.

```
cd /path/to/your/app
sudo docker build -t myapp:latest .
```

이 명령어는 현재 디렉토리에 있는 Dockerfile을 사용하여 `myapp`이라는 이름과 `latest` 태그를 가진 이미지를 빌드한다.

### 3. Docker 컨테이너 실행

빌드된 이미지를 사용하여 컨테이너를 실행한다. `-d` 옵션은 컨테이너를 백그라운드에서 실행하며, `-p` 옵션은 호스트와 컨테이너 간의 포트를 매핑한다.

```
sudo docker run -d -p 5000:5000 myapp:latest
```

## 프로세스 vs 도커 컨테이너

### 도커 컨테이너는 프로세스와 유사하다

- 도커 컨테이너는 실제로 하나 이상의 프로세스를 실행하는 격리된 환경이다.
- 각 컨테이너는 독립된 네임스페이스와 리소스를 사용하여 격리된 상태에서 실행된다.
자원 할당과 관리: 도커는 CPU, 메모리, I/O 등의 자원을 관리하고 할당한다.
- 자원 제한이나 우선 순위는 사용자가 설정한 도커 설정에 따라 결정된다.
- 예를 들어, docker run 명령어에서 --memory나 --cpus 옵션을 사용하여 자원을 제한할 수 있다.

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

## [실습] 도커 이미지 만들기 (로컬 리눅스에서 실행)

- 도커가 없을 경우 설치

```bash
sudo apt install docker.io
```

```bash
$ mkdir ~/docker
$ cd ~/docker
```

`echo_docker[.sh](http://echo.sh/)`

```bash
#!/bin/bash
echo "Hello, Docker!"
```

```bash
$ chmod +x echo_docker[.sh](http://echo.sh/)
```

`Dockerfile`

```bash
# 베이스 이미지 선택
FROM alpine:latest

# bash 설치
RUN apk add --no-cache bash

# 작업 디렉토리 설정
WORKDIR /app

# 로컬의 echo_docker.sh 스크립트를 컨테이너의 /app 디렉토리에 복사
COPY echo_docker.sh .

# 실행 권한 부여
RUN chmod +x echo_docker.sh

# 컨테이너가 실행될 때 실행할 명령어 지정
CMD ["bash", "./echo_docker.sh"]
```

## 이미지 빌드

```bash
$ sudo docker build --no-cache -t my-echo-app:latest .
```

## 이미지 확인

```bash
$ sudo docker images
```

## 이미지 실행

```bash
$ sudo docker run --rm my-echo-app
```

## (c.f) 사용하지 않는 이미지 삭제

```bash
$ sudo docker rmi <id>
```

- 도커 주의 사항 (용량)

    - [https://csj000714.tistory.com/603](https://csj000714.tistory.com/603)