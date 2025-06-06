# [실습] 리다이렉션 - 10분

## 실습 전 준비

```bash
$ cat <<EOL > system.log
2023-07-13 10:05:00 [WARN] Low disk space
2023-07-13 10:20:00 [INFO] User logout: user1
2023-07-13 10:00:00 [INFO] System started
2023-07-13 10:10:00 [ERROR] Disk read failure
2023-07-13 10:25:00 [ERROR] Network timeout
2023-07-13 10:30:00 [INFO] System shutdown
2023-07-13 10:15:00 [INFO] User login: user1
EOL
```

---

## 실습 단계

1. `system.log`에서 `INFO`가 포함된 줄만 찾아 `info.log` 파일로 저장해보자  

2. `info.log` 파일 끝에 "Log file created"라는 메시지를 추가해보자  

3. `system.log` 파일을 시간순으로 정렬한 뒤 `sorted`라는 파일로 저장해보자  
