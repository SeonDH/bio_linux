
## [실습] nohup - 5분

## 실습 전 준비

```bash
mkdir -p ~/nohup
cd ~/nohup
```

### 스크립트 작성: `create_log_file.sh`

```bash
#!/bin/bash
LOG_FILE="logfile.txt"
while true; do
  echo "Log entry $(date)" >> "$LOG_FILE"
  sleep 1
done
```

### 실행 권한 부여

```bash
chmod +x create_log_file.sh
```

`nohup ./create_log_file.sh > output.log 2>&1 &` 명령어로 **백그라운드 실행**한다.

## 실습 단계


2. `jobs`로 **작업을 확인**한다.
3. `exit` 명령어로 **세션을 종료**한다.
4. 다시 로그인한 후, `tail logfile.txt`로 **작업이 계속되었는지 확인**한다. (시간이 충분하지 않다면 작업이 계속 될 수 있음)
5. 
