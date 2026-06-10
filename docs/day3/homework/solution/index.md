# Day 3 과제 답지 예시

## 1. GitHub 가입

[https://github.com](https://github.com)에서 계정을 만든 뒤 로그인까지 확인한다.

## 2. 권한 변경

```bash
touch permission
chmod 644 permission
ls -l permission
```

`rw-r--r--`는 소유자는 읽기/쓰기 가능, 그룹과 다른 사용자는 읽기만 가능한 권한이다.

## 3. 프로세스 확인과 종료

```bash
vi process.sh
```

입력 내용:

```bash
#!/bin/bash
for i in {1..10}; do
  echo "현재 사용자: $USER"
  sleep 3
done
```

실행과 확인:

```bash
chmod +x process.sh
./process.sh &
jobs
ps -ef | grep process.sh
```

종료:

```bash
kill %1
```

`jobs`에서 작업 번호가 다르게 보이면 해당 번호로 바꿔서 실행한다.

## 4. `scp`로 로컬 Linux에 복사

로컬 Linux 터미널에서 실행한다.

```bash
scp user@server_ip:/home/user/process.sh ~/process.sh
ls -l ~/process.sh
```

`user`, `server_ip`, 원격 경로는 본인 환경에 맞게 바꾼다.
