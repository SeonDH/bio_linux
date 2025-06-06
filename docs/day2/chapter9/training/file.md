# [실습] 파일 찾기 - 10분

## 실습 전 준비

```bash
$ touch file1.txt file2.log file3.txt file4.doc file5.txt
$ dd if=/dev/zero of=medium_file.txt bs=1K count=10
$ dd if=/dev/zero of=large_file.txt bs=1M count=1
```

---

## 실습 단계

1. `.txt` 확장자를 가지고 있는 파일을 찾으세요.

2. 이름에 `file`이 포함된 파일을 찾으세요.

3. 크기가 10KB 초과인 파일을 찾으세요.

4. 크기가 10KB 미만인 파일을 찾으세요.