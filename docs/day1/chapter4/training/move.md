# [실습] 디렉터리 이동 - 10분

이 실습에서는 상대 경로와 절대 경로를 활용해 디렉터리를 이동하는 방법을 익힌다. 또한 현재 위치 확인과 디렉터리 내 파일 목록 확인 방법도 함께 실습한다.


## 실습 전 준비

```bash
$ mkdir -p ~/first/second/third/fourth
$ cd ~/first/second
```

`~/first/second/third/fourth` 구조를 사전에 만들어 두고, `~/first/second`에서 실습을 시작한다.


## 실습 단계

### 1. 현재 작업 디렉터리 확인

- 현재 내가 위치한 디렉터리가 어디인지 확인해본다.



### 2. 상대 경로로 하위 디렉터리 이동

- 현재 위치에서 `fourth` 디렉터리까지 상대 경로를 이용하여 이동해본다.



### 3. 홈 디렉터리로 상대 경로 이동

- `fourth` 디렉터리에서 `~` 기호를 활용하여 홈 디렉터리로 이동해본다.



### 4. 절대 경로로 이동

- `/bin` 디렉터리로 절대 경로를 이용하여 이동해본다.



### 5. 디렉터리 파일 목록 확인

- `/bin` 디렉터리 내 모든 파일과 상세 정보를 확인해본다.
