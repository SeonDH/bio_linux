
# [실습] nohup - 5분

## 실습 전 준비

```bash
mkdir -p ~/nohup
cd ~/nohup
```

### 스크립트 작성: `create_log_file.sh`

```bash
#!/bin/bash
LOG_FILE="logfile.txt"
for i in {1..30}; do
  echo "Log entry $(date)" >> "$LOG_FILE"
  sleep 1
done
```

### 실행 권한 부여

```bash
chmod +x create_log_file.sh
```

## 실습 단계

### 1. `bg` 방식으로 실행해보기

먼저 일반 백그라운드 작업 제어를 확인한다.

```bash
./create_log_file.sh
```

실행 중 `Ctrl + Z`를 눌러 작업을 일시 중지한다.

```bash
jobs
bg %1
jobs
kill %1
```

`bg`로 실행한 작업은 `jobs`에서 확인할 수 있는 현재 셸의 작업이다.

### 2. `nohup`으로 실행하고 PID 남기기

```bash
nohup ./create_log_file.sh > output.log 2>&1 & echo $! > create_log_file.pid
```

- `$!`는 바로 직전에 백그라운드로 실행한 프로세스의 PID이다.
- PID를 파일에 저장해두면 나중에 `ps`로 확인하고 `kill`로 종료할 수 있다.

PID가 파일에 저장되었는지 확인한다.

```bash
cat create_log_file.pid
ps -p $(cat create_log_file.pid) -o pid,ppid,stat,cmd
```

로그가 계속 쌓이는지 확인한다.

```bash
timeout 10s tail -f logfile.txt
```

`tail`은 10초 뒤 자동 종료된다. `create_log_file.sh`는 최대 30초 동안 실행된 뒤 자동 종료된다.

### 3. `nohup`과 `bg` 차이 확인

```bash
jobs
```

터미널을 새로 열거나 다시 로그인한 뒤 같은 디렉터리로 이동해서 확인한다.

```bash
cd ~/nohup
jobs
ps -p $(cat create_log_file.pid) -o pid,ppid,stat,cmd
tail logfile.txt
```

- `jobs`는 현재 셸에서 시작한 작업만 보여준다.
- `nohup`으로 실행한 작업은 새 터미널의 `jobs`에는 보이지 않을 수 있다.
- PID 파일을 남겨두면 `ps`와 `kill`로 프로세스를 직접 관리할 수 있다.
- 30초가 지나면 예제 스크립트가 자동 종료될 수 있다.

### 4. `nohup` 프로세스 종료

```bash
kill $(cat create_log_file.pid)
sleep 1
ps -p $(cat create_log_file.pid)
rm -f create_log_file.pid
```

`ps` 결과에 프로세스가 나오지 않으면 종료된 것이다.

## 답지

- [답지 예시](../solution/nohup_solution.md)
