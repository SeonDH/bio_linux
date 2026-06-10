# [답지] 쉘 명령어와 환경 변수 체험

## 1. 명령어 종류 확인

```bash
type cd
type ls
type echo
type man
```

보통 `cd`, `echo`는 셸 내장 명령어이고, `ls`, `man`은 외부 명령어로 확인된다.

## 2. 환경 변수 설정 및 확인

```bash
export MY_NAME="linux_user"
echo "$MY_NAME"

unset MY_NAME
echo "$MY_NAME"
```

영구 설정 예시:

```bash
vi ~/.bashrc
```

아래 줄을 추가한다.

```bash
export MY_NAME="linux_user"
```

적용:

```bash
source ~/.bashrc
echo "$MY_NAME"
```
