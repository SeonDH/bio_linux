# [실습] 파일 권한 변경 - 5분

## 실습 전 명령어

```bash
mkdir -p ~/file_auth
cd ~/file_auth
echo -e '#!/bin/bash\necho "Hello, World!"' > hello.sh
chmod +x hello.sh
```

---

## 실습 문제

1. `hello.sh` 파일의 권한을 확인한다.
2. `hello.sh` 파일을 실행한다.
3. `hello.sh` 파일의 소유자에게 실행 권한을 추가한다.
4. 다시 `hello.sh` 파일을 실행한다.
