# [답지] 파일 권한 변경

권한 확인:

```bash
ls -l hello.sh
```

실행 시도:

```bash
./hello.sh
```

실행 권한이 없으면 `Permission denied`가 출력될 수 있다.

소유자에게 실행 권한 추가:

```bash
chmod u+x hello.sh
ls -l hello.sh
```

다시 실행:

```bash
./hello.sh
```
