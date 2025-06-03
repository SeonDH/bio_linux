# [번외] Homebrew

- macOS 용 패키지 관리자

### Homebrew의 특징

1. **편리한 설치 및 관리**: 터미널 명령어로 쉽게 패키지를 설치, 업데이트, 삭제할 수 있습니다.
2. **광범위한 패키지 지원**: 수천 개의 패키지를 지원하며, 다양한 개발 도구와 라이브러리를 포함하고 있습니다.
3. **의존성 관리**: 패키지를 설치할 때 필요한 의존성도 자동으로 설치해줍니다.

## Homebrew 설치 방법

### 1. 터미널을 이용한 방법

1. 터미널을 연다
2. 다음 명령어를 실행
    
    ```
    /bin/bash -c "$(curl -fsSL <https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh>)"
    ```
    
3. 설치가 완료되면 `brew` 명령어를 사용하여 Homebrew를 사용할 수 있다.

### 2. 홈페이지에서 직접 다운로드

## Homebrew 사용 방법

- **패키지 검색**: 패키지를 검색할 수 있습니다.
    
    ```
    brew search [패키지명]
    ```
    
- **패키지 설치**: 원하는 패키지를 설치할 수 있습니다.
    
    ```
    brew install [패키지명]
    ```
    
- **설치된 패키지 목록 확인**: 설치된 패키지의 목록을 확인할 수 있습니다.
    
    ```
    brew list
    ```
    
- **패키지 업데이트**: 설치된 패키지를 업데이트할 수 있습니다.
    
    ```
    brew upgrade [패키지명]
    ```
    
- **패키지 삭제**: 설치된 패키지를 삭제할 수 있습니다.
    
    ```
    brew uninstall [패키지명]
    ```
    
- **Homebrew 자체 업데이트**: Homebrew 자체를 최신 버전으로 업데이트할 수 있습니다.
    
    ```
    brew update
    ```
    

## Homebrew의 주요 명령어 정리

- `brew install [패키지명]`: 패키지 설치
- `brew uninstall [패키지명]`: 패키지 삭제
- `brew upgrade [패키지명]`: 패키지 업데이트
- `brew list`: 설치된 패키지 목록 확인
- `brew update`: Homebrew 업데이트
- `brew search [패키지명]`: 패키지 검색