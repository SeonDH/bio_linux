# [답지] ps 실습

실행 중인 프로세스 확인:

```bash
ps -ef | grep sleep_script.sh
```

출력에서 `sleep_script.sh`를 실행 중인 줄의 PID를 확인한다.

예를 들어 PID가 `12345`라면 아래처럼 종료한다.

```bash
kill 12345
```

다시 확인:

```bash
ps -ef | grep sleep_script.sh
```
