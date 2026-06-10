# [답지] nohup

## 1. `bg` 방식 확인

```bash
./create_log_file.sh
```

실행 중 `Ctrl + Z`를 누른 뒤 아래 명령어를 실행한다.

```bash
jobs
bg %1
jobs
kill %1
```

## 2. `nohup` 실행

```bash
nohup ./create_log_file.sh > output.log 2>&1 &
echo $! > create_log_file.pid
```

확인:

```bash
cat create_log_file.pid
ps -p $(cat create_log_file.pid) -o pid,ppid,stat,cmd
timeout 10s tail -f logfile.txt
```

## 3. 종료

```bash
kill $(cat create_log_file.pid)
sleep 1
ps -p $(cat create_log_file.pid)
rm -f create_log_file.pid
```
