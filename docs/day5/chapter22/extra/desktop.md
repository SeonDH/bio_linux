# [번외] macOS와 Windows에서 Dockerfile 사용하기

본 장의 기본 실습은 로컬 Linux에서 Docker Engine을 사용하는 흐름을 기준으로 한다.
macOS와 Windows에서는 Docker Desktop을 설치하면 같은 `Dockerfile`, `docker build`, `docker run` 흐름을 사용할 수 있다.

> 라이선스 주의: Docker Desktop은 개인 사용, 교육, 소규모 조직 등에는 무료로 사용할 수 있지만, Docker가 정한 규모를 넘는 기업의 상업적 사용에는 유료 구독이 필요할 수 있다. 회사 장비에서 설치하는 경우에는 기관의 소프트웨어 사용 정책과 [Docker Desktop 라이선스](https://docs.docker.com/subscription/desktop-license/)를 확인한다.

## macOS

1. Docker Desktop for Mac을 설치한다.
2. 설치 후 Docker Desktop을 실행한다.
3. 상단 메뉴바에 Docker 아이콘이 표시되고 실행 상태가 될 때까지 기다린다.
4. Terminal에서 아래 명령어를 실행한다.

```bash
docker --version
docker run --rm hello-world
```

Apple Silicon(M1/M2/M3) Mac과 Intel Mac은 설치 파일이 다를 수 있으므로 본인 장비에 맞는 버전을 선택한다.

Dockerfile이 있는 디렉터리에서 이미지를 빌드하고 실행한다.

```bash
cd ~/docker_batch
docker build -t bio-batch-demo:latest .
docker run --rm bio-batch-demo:latest
```

## Windows

1. Docker Desktop for Windows를 설치한다.
2. 설치 과정에서 WSL 2 사용 안내가 나오면 안내에 따라 WSL 2를 활성화한다.
3. 설치 후 Docker Desktop을 실행한다.
4. PowerShell 또는 MobaXterm 로컬 터미널에서 아래 명령어를 실행한다.

```powershell
docker --version
docker run --rm hello-world
```

Windows에서는 Docker Desktop이 실행 중이어야 `docker` 명령어가 정상 동작한다.

Dockerfile이 있는 디렉터리에서 이미지를 빌드하고 실행한다.

```powershell
cd docker_batch
docker build -t bio-batch-demo:latest .
docker run --rm bio-batch-demo:latest
```

## 리눅스 실습과 다른 점

Dockerfile 자체는 Linux, macOS, Windows에서 거의 동일하게 사용할 수 있다.
다만 경로 표기와 파일 공유 방식은 운영체제에 따라 차이가 날 수 있다.

| 항목 | Linux | macOS/Windows |
| --- | --- | --- |
| Docker 실행 방식 | Docker Engine | Docker Desktop |
| 경로 예시 | `/home/user/docker_batch` | macOS: `/Users/user/docker_batch`, Windows: `C:\Users\user\docker_batch` |
| 실행 전 확인 | `systemctl status docker` | Docker Desktop 실행 여부 확인 |

