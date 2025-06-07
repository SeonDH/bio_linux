# [번외] 자주 나오는 오류 (Windows)

실습 도중 아래와 같은 오류가 발생할 수 있다.  
주로 Windows 사용자에게 해당되며, Mac 사용자는 대부분 무관하다.


## 1. Visual Studio C++ 런타임 누락 오류

### 증상

리눅스 가상머신을 실행했을 때 아래와 같은 오류가 뜨는 경우:

<img src="../images/Untitled%2013.png" width="60%">

### 원인

Visual Studio C++ 런타임(Visual C++ Redistributable)이 설치되지 않아서 발생한다.

### 해결 방법

1. 아래 링크에서 최신 버전의 Visual C++ Redistributable 설치
2. 시스템 재부팅 후 다시 VirtualBox 실행

[Microsoft 공식 다운로드 링크](https://learn.microsoft.com/ko-kr/cpp/windows/latest-supported-vc-redist?view=msvc-170)


## 2. 가상화 설정 비활성화 오류

### 증상

가상머신을 실행하려고 할 때 아래와 같은 메시지가 나타난다:

- "VT-x is not available"
- "AMD-V is disabled in BIOS"
- "Hardware virtualization is not enabled"

<img src="../images/Untitled%2014.png" width="60%">


### 2-1. BIOS에서 가상화 기술 활성화

가상화 기능이 BIOS에서 꺼져 있을 경우 수동으로 켜야 한다.

#### 해결 방법

1. 컴퓨터 재부팅 → BIOS/UEFI 진입  
   (일반적으로 부팅 중 `F2`, `F10`, `Del`, `ESC` 키 중 하나)

2. 아래와 같은 설정 항목을 Enabled 상태로 변경
   - Virtualization Technology
   - Intel VT-x, Intel VT-d
   - AMD-V, SVM Mode 등

3. 변경 사항 저장 후 시스템 재부팅

※ Windows 11에서는 "설정 > 시스템 > 복구 > 고급 시작 > UEFI 설정"으로도 BIOS 진입 가능


### 2-2. Hyper-V 비활성화

Windows의 Hyper-V 기능이 켜져 있으면 VirtualBox와 충돌할 수 있다.

#### 해결 방법 (GUI)

1. 시작 메뉴 → "Windows 기능 켜기/끄기" 검색 후 실행  
2. 아래 항목의 체크를 모두 해제
   - Hyper-V
   - 가상 머신 플랫폼
   - Windows 하이퍼바이저 플랫폼

3. 확인 후 재부팅

#### 해결 방법 (명령어)

아래 명령어를 입력하면 Hyper-V 자동 실행을 비활성화할 수 있다:

```bash
bcdedit /set hypervisorlaunchtype off
```

Hyper-V를 다시 사용하고 싶은 경우
VirtualBox 실습이 끝난 뒤 Hyper-V 기반의 WSL2 또는 기타 기능을 다시 사용하고 싶다면, 아래 명령어로 원복할 수 있다:

```bash
bcdedit /set hypervisorlaunchtype auto
```