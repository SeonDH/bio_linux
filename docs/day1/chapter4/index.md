---
title: "4. 디렉터리 및 파일 기본 명령어"
nav_order: 10
layout: default
---

# 4. 디렉터리 및 파일 기본 명령어

## 리눅스 서버 접근

- 실제 서버 접근 예시:

```bash
ssh user{}@koreabio.limeops.co.kr -p 1119 -o Ciphers=aes256-cbc 
```

> 명령어 해석: 
SSH 프로토콜을 사용해서 koreabio.limeops.co.kr 서버에, 사용자 user{}의 계정으로 1119 포트를 통해 접속하되, 암호화 방식은 aes256-cbc만 허용해서 접속할 거야.

- 로컬 리눅스 서버 접근:

  - [번외: mobaxterm 사용 (ssh)](extra/mobaxterm.md)
  - [번외: ssh로 로컬 리눅스 서버 접근](extra/ssh.md)

- 리눅스 명령어 팁
  - [번외: 리눅스 명령어 팁 모음](extra/tip.md)

## 기본 명령어

### `pwd`: 현재 작업 디렉터리 출력 - print working directory

```bash
$ pwd
/home/localhost
```


### `cd`: 디렉터리 이동 - change directory

- . 은 현재 내 경로를 의미 (생략 가능)
- .. 은 내 상위 경로를 의미

```bash
$ cd /tmp              # 절대 경로로 이동. /tmp 디렉토리로 이동한다.
$ cd ~                 # 홈 디렉터리로 이동. ~ 디렉토리는 사용자의 홈 디렉토리를 의미한다.
$ cd ..                # 상위 디렉터리로 이동. (상대경로)
$ cd localhost         # 현재 디렉터리 하위로 이동. 현재 디렉토리 하위의 localhost 디렉토리로 이동한다. (상대 경로)
$ cd ../../home        # 두 단계 상위에서 하위로 이동. 현재 디렉토리의 상위 디렉토리의 상위 디렉토리의 하위 home 디렉토리로 이동한다. (상대 경로)
$ cd                   # 홈 디렉터리로 이동
```

### `ls`: 디렉터리 목록 확인 - list

```bash
$ ls                   # 기본 목록
$ ls -a                # 숨김 파일 포함
$ ls -F                # 파일 종류 표시
$ ls -l                # 상세 정보
$ ls -alF              # 조합 사용
$ ll                   # ls -alF의 alias. 사람들이 자주 사용하는 ls -alF 와 같은 경우는 리눅스 시스템에서 자체적으로 alias 라는 개념으로 명령어를 더 쉽게 사용할 수 있도록 설정
$ alias                # alias 확인. alias 명령어를 통해 어떤 alias 가 걸려있는지 알 수 있다.
$ dir, vdir            # ls 유사 명령어. (도스 명령어에 익숙한 사용자들을 위해 제공)
```

## [실습] 디렉터리 이동 (10분)

- [실습: 디렉터리 이동 - 10분](training/move.md)



### `mkdir`: 디렉터리 생성 - make directory

```bash
$ mkdir test                     # 현재 위치에 test 디렉터리 생성
$ mkdir /home/localhost/test     # 절대 경로 /home/localhost/ 디렉터리에 test 디렉터리 생성
$ mkdir ../test                  # 상위 디렉터리에 test 디렉터리 생성
$ mkdir test1 test2 test3        # 여러 개 한번에 생성
$ mkdir -p /a/b/c                # 중간 디렉터리가 없을 경우 자동으로 생성 (-p 옵션)
```

### `rmdir`: 빈 디렉터리 삭제 - remove directory

```bash
$ rmdir test                     # 빈 디렉터리 삭제
$ rmdir test1 test2 test3        # 여러 개 삭제
$ rmdir -p /a/b/c                # 상위 포함 삭제 (부모 디렉터리가 비어있을 경우 같이 삭제도 가능)
```

### `touch`: 빈 파일 생성 or 타임스탬프 갱신 - 파일을 "접촉"하여 타임스탬프를 업데이트한다는 의미에서 유래

```bash
$ touch test                     # 새 파일 생성. 이미 생성된 파일인 경우 타임스탬트를 업데이트 한다
$ touch test1 test2 test3        # 여러 개 생성
$ touch /path/to/file            # 절대 경로
```

### `cp`: 파일 복사 - copy

```bash
$ cp test test_copy              # 동일 디렉터리 복사. 현재 디렉터리의 test 파일을 복사하여 test_coped 파일을 생성
$ cp /a/test /b/test_copy        # 절대 경로 복사
```

### `mv`: 파일 이동 또는 이름 변경 - move

```bash
$ mv test test_new               # 이름 변경. test 파일의 이름을  test_new 로 수정
$ mv test ../                    # 상위로 이동
$ mv test ../test_new            # 이동하면서 이름 변경
```

### `rm`: 파일 및 디렉터리 삭제 - remove

**rm 명령어는 매우 강력한 명령어로 리눅스 시스템 파일도 날릴 수 있어서 조심히 날려야한다. 되돌릴 수 없는 명령어이다. (휴지통이 없다)**

```bash
$ rm test                        # 기본 삭제. 현재 디렉터리의 test 를 삭제
$ rm -i test                     # 확인 요청. 정말로 삭제할껀지 물어보게 할 수 있다
$ rm -r test                     # 디렉터리 포함 삭제
$ rm -f test                     # 강제 삭제. 메시지를 무시하고 바로 삭제
$ rm -rf test                    # 묻지도 않고 삭제. 강력한 삭제 메시지. 묻지도 따지지도 않고 모두 삭제하기 때문에 삭제하면 안 되는 파일도 삭제될 확률이 높다
```

#### `rmdir` vs `rm -r`

| 명령어     | 특징                           |
|------------|--------------------------------|
| `rmdir`    | 빈 디렉터리만 삭제 가능        |
| `rm -r`    | 하위 내용 포함 모두 삭제 가능  |

## [실습] 디렉터리 및 파일 생성 제거 (10분)

- [실습: 디렉터리 및 파일 생성/제거 - 10분](training/create_delete.md)


## 명령어 요약

| 명령어 | 설명                         |
|--------|------------------------------|
| `pwd`  | 현재 디렉터리 출력           |
| `cd`   | 디렉터리 이동                |
| `ls`   | 디렉터리 목록 보기           |
| `mkdir`| 디렉터리 생성                |
| `rmdir`| 빈 디렉터리 삭제             |
| `touch`| 빈 파일 생성 또는 갱신       |
| `cp`   | 파일 복사                    |
| `mv`   | 파일 이동 또는 이름 변경     |
| `rm`   | 파일 또는 디렉터리 삭제      |

## 참고

- 각 명령어에 대해서 자세히 알고 싶다면?
  - [번외: `man` 명령어와 --help 옵션](extra/man.md)
- 우리가 명령어를 날렸을 때 어떻게 처리가 되는지 궁금하다면?
  - [번외: 리눅스 명령어 처리 과정](extra/process.md)

## 요약

1. `pwd`, `cd`, `ls` 등으로 현재 위치 및 디렉터리 상태를 확인할 수 있다.
2. `mkdir`, `rmdir`, `rm -r` 명령으로 디렉터리를 생성하거나 삭제할 수 있다.
3. `touch`, `cp`, `mv`, `rm` 등으로 파일을 조작할 수 있다.
4. `rm -rf` 등 위험한 명령어는 신중히 사용해야 한다.
