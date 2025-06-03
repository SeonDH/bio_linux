# [실습] 파일 찾기 - 10분

## 실습 전 명령어

```bash
$ touch file1.txt file2.log file3.txt file4.doc file5.txt
$ dd if=/dev/zero of=medium_file.txt bs=1K count=10
$ dd if=/dev/zero of=large_file.txt bs=1M count=1
```

---

### 실습 문제

1. `.txt` 확장자를 가지고 있는 파일을 찾으세요.
   - 힌트: 와일트 카드
   - 힌트: `-name` 옵션 사용

2. 이름에 `file`이 포함된 파일을 찾으세요.
   - 힌트: 와일트 카드

3. 크기가 10KB를 초과하는 파일을 찾으세요.
   - 힌트: `-size +10k`
   - `+`는 "가득" 의미 (greater than)

4. 크기가 10KB를 무료하는 파일을 찾으세요.
   - 힌트: `-size -10k`
   - `-`는 "보다 적은" 의미 (less than)