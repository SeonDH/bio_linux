---
title: "22. 도커(docker)"
nav_order: 28
layout: default
---

# 22. 도커 (docker)

## Docker란?

- 애플리케이션과 그 종속성을 **컨테이너**라는 경량 가상 환경에 패키징해 어디서나 일관되게 실행할 수 있도록 돕는 플랫폼  
- 개발·테스트·배포·운영 환경 간 차이를 최소화해 “로컬에서 잘 되던 코드가 서버에서 안 돼요” 문제를 방지  

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

-  애플리케이션 격리
    - Docker는 컨테이너를 사용하여 애플리케이션을 격리된 환경에서 실행한다. 이는 다른 애플리케이션과의 충돌을 방지하고, 일관된 실행 환경을 제공한다.
- 효율적인 리소스 사용
    - Docker는 호스트 시스템의 커널을 공유하여 가상 머신보다 더 효율적으로 리소스를 사용한다. 이는 컨테이너의 빠른 시작과 적은 오버헤드를 가능하게 한다.
- 이식성
    - Docker 이미지는 한 번 빌드하면 어디서나 실행할 수 있다. 이는 개발, 테스트, 운영 환경 간의 일관성을 유지하는 데 도움을 준다.
- 빠른 배포
    - Docker는 애플리케이션을 패키징하고 배포하는 과정을 단순화한다. 컨테이너는 빠르게 시작되고, 애플리케이션의 배포 시간을 단축할 수 있다.

## Docker의 동작 방식

1. 이미지 빌드
    사용자는 Dockerfile을 작성하여 이미지를 빌드한다. Docker는 Dockerfile을 읽고, 명령어를 순차적으로 실행하여 이미지를 생성한다.
    ```
    docker build -t myapp .
    ```
2. 컨테이너 실행
    이미지로부터 컨테이너를 생성하고 실행한다. 사용자는 필요한 설정을 지정하여 컨테이너를 실행할 수 있다.
    ```
    sudo docker run -d -p 8080:80 myapp
    ```
3. 컨테이너 관리
    사용자는 실행 중인 컨테이너를 관리할 수 있다. 컨테이너를 일시 정지, 중지, 재시작할 수 있으며, 로그를 확인할 수 있다.
    ```
    sudo docker ps            # 실행 중인 컨테이너 목록 보기
    sudo docker stop myapp    # 컨테이너 중지
    sudo docker start myapp   # 컨테이너 시작
    sudo docker logs myapp    # 컨테이너 로그 보기
    ```

## Dockerfile 빌드 및 실행 방법

1. Docker 설치
    ```
    sudo apt-get update
    sudo apt-get install -y docker.io
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

2. Dockerfile 빌드
    - Dockerfile이 있는 디렉토리로 이동하여 이미지를 빌드한다. `-t` 옵션을 사용하여 이미지를 태그할 수 있다.
    - 이 명령어는 현재 디렉토리에 있는 Dockerfile을 사용하여 `myapp`이라는 이름과 `latest` 태그를 가진 이미지를 빌드한다.

    ```
    cd /path/to/your/app
    sudo docker build -t myapp:latest .
    ```

3. Docker 컨테이너 실행

    - 빌드된 이미지를 사용하여 컨테이너를 실행한다. `-d` 옵션은 컨테이너를 백그라운드에서 실행하며, `-p` 옵션은 호스트와 컨테이너 간의 포트를 매핑한다.
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


- `echo_docker.sh` 파일 작성
```bash
#!/bin/bash
echo "Hello, Docker!"
```

```bash
$ chmod +x echo_docker.sh
```

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

- `Dockerfile` 파일 생성
    - Alpine Linux 기반 컨테이너를 만들고
    - bash를 설치한 뒤
    - /app 디렉터리에 로컬 스크립트를 복사·실행 권한을 주고
    - 컨테이너가 시작되면 그 스크립트를 bash로 실행하도록 설정


- 이미지 빌드
    ```bash
    $ sudo docker build --no-cache -t my-echo-app:latest .
    ```

- 이미지 확인

    ```bash
    $ sudo docker images
    ```

- 이미지 실행

    ```bash
    $ sudo docker run --rm my-echo-app
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
    $ sudo docker rmi <id>
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
    - `sudo docker images` 에서 용량 확인
    - [https://csj000714.tistory.com/603](https://csj000714.tistory.com/603)