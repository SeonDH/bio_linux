# [실습] ps 실습 - 10분

## 실습 전 준비

```bash
mkdir -p ~/ps
cd ~/ps
echo '#!/bin/bash
echo "Starting to sleep for 100 seconds..."
sleep 100
echo "Finished sleeping."' > sleep_script.sh
chmod +x sleep_script.sh
./sleep_script.sh &
```

---

## 실습 단계

1. 실행 중인 프로세스 목록에서 `sleep_script.sh` 프로세스를 확인한다.
2. 해당 프로세스를 종료한다.