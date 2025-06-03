다음은 `[번외] APT Repository 추가` 챕터에 대해 리눅스 교재 스타일에 맞춰 **문체 통일**, **구조 정비**, **표현 명료화**를 적용한 리팩토링입니다. 그대로 복사해 사용하셔도 좋습니다.

---

# \[번외] APT 저장소(Repository) 추가

APT 저장소(Repository)는 패키지 관리 도구가 소프트웨어를 다운로드하고 설치할 수 있는 서버 위치이다. 새로운 소프트웨어를 설치하거나 최신 버전을 사용하려면, 시스템에 저장소를 추가해야 할 수 있다.

---

## 1. PPA(Personal Package Archive) 저장소 추가

* `add-apt-repository` 명령어를 사용하여 Launchpad 기반 PPA 저장소를 추가한다.

```bash
sudo add-apt-repository ppa:repository_name
sudo apt update
```

* 저장소가 추가되면 자동으로 패키지 목록을 갱신한다.
* 이후 `apt install` 명령어로 해당 PPA에 있는 소프트웨어를 설치할 수 있다.

---

## 2. 일반 URL 기반 저장소 추가

PPA가 아닌 일반 저장소는 다음 두 가지 방식으로 추가할 수 있다:

---

### 방법 1: `/etc/apt/sources.list` 파일 직접 수정

```bash
sudo nano /etc/apt/sources.list
```

* 아래 형식의 줄을 추가한다:

```bash
deb [arch=amd64] http://repository_url/ubuntu focal main
```

* 저장한 후 패키지 목록을 갱신한다:

```bash
sudo apt update
```

---

### 방법 2: `.list` 파일 생성 (권장)

* `/etc/apt/sources.list.d/` 디렉토리에 `.list` 파일을 만들어 저장소를 추가한다:

```bash
echo "deb [arch=amd64] http://repository_url/ubuntu focal main" \
  | sudo tee /etc/apt/sources.list.d/custom-repo.list
sudo apt update
```

---

## 주의사항

* 저장소에 따라 GPG 키 추가가 필요할 수 있다. 이 경우 `apt-key` 또는 `gpg`, `signed-by` 옵션 등을 추가로 설정해야 한다.
* 우분투 버전에 맞는 코드네임(`focal`, `jammy` 등)을 정확히 사용해야 한다.

---

## 요약

| 작업           | 명령어                                      |
| ------------ | ---------------------------------------- |
| PPA 저장소 추가   | `sudo add-apt-repository ppa:...`        |
| 일반 저장소 직접 등록 | `/etc/apt/sources.list` 또는 `.list` 파일 생성 |
| 목록 갱신        | `sudo apt update`                        |
