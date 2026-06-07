---
title: "0. 시작하기에 앞서"
nav_order: 6
layout: default
---

# 0. 시작하기에 앞서

## 강의 목표

이 강의가 끝난 후 여러분은 다음과 같은 역량을 갖추게 됩니다.

- 리눅스의 개념과 작동 원리를 이해하고, 간단한 명령어를 사용할 수 있다.
- vi 편집기를 활용하여 텍스트 파일을 작성 및 수정할 수 있다.
- 파일의 내용을 확인하고 필요한 정보를 추출할 수 있다.
- 외부 리눅스 서버에 접속하여 원격으로 명령을 실행할 수 있다.
- 셸(Shell)의 개념을 이해하고 간단한 셸 스크립트를 작성할 수 있다.
- 파일 권한을 설정할 수 있으며, 프로세스를 확인 및 제어할 수 있다.
- 파일을 리눅스 ↔ 로컬 PC 간 전송할 수 있다.
- Git, Conda, Docker 등 개발 도구의 기본 개념을 이해한다.


## 강의 자료

- Ubuntu 24.04 기준으로 교재가 작성되어있다.


## 실습 준비: 파일 다운로드

### 1. Ubuntu Server 다운로드

<img src="images/ubuntu.png" alt="Ubuntu 설치 화면" width="60%">


터미널 기반 실습만 진행하므로 **Desktop 버전이 아닌 Server 버전**을 다운로드한다.  
GUI가 없어 자원을 더 효율적으로 사용할 수 있다.



- Windows, Intel Mac: [https://ubuntu.com/download/server](https://ubuntu.com/download/server)
- M1 Mac (ARM): [https://ubuntu.com/download/server/arm](https://ubuntu.com/download/server/arm)



### 2. 가상 머신 설치

강의에서는 UTM을 기준으로 설명하지만, 다른 가상 머신도 사용 가능하다.

- UTM (Mac 추천, 특히 M1): [https://mac.getutm.app/](https://mac.getutm.app/)
- VirtualBox (Windows 추천): [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
- 기타: VMware, LSM 등

### 3. Windows의 경우 MobaXterm 설치 후 터미널 사용 (macOS의 경우 기본 터미널 사용)

- Windows: [MobaXterm](https://mobaxterm.mobatek.net/download-home-edition.html)을 설치한 뒤, SSH 접속과 터미널 실습에 사용한다.
- macOS: 기본 Terminal 앱을 사용한다.

원격 Linux 서버에 접속하는 실습은 MobaXterm 기준으로 진행한다.

### 4. 설치 페이지 광고 주의

검색 결과의 광고 링크를 통해 설치 페이지에 들어가는 경우가 있다.  
이때는 주소창의 도메인이 공식 사이트와 정확히 일치하는지 확인하고, 의심스러우면 공식 주소를 직접 입력해서 접속한다.

- [번외: 설치 페이지 광고와 피싱 주의](extra/install_warning.md)
