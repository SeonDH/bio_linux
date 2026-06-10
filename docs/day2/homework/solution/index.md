# Day 2 과제 답지 예시

## 1. `vi` 실습

```bash
vi vi_practice.txt
```

예시 흐름:

1. Line 1 아래에서 `o`를 누르고 Line 1 내용을 입력한다.
2. Line 6으로 이동한 뒤 `2dd`로 2줄을 삭제한다.
3. `u`로 삭제 작업을 취소한다.
4. Line 5에서 `yy`로 복사하고 Line 8 아래에서 `p`로 붙여넣는다.
5. Line 6에서 `:s/line/LINE/g`로 해당 줄의 `line`을 `LINE`으로 바꾼다.
6. `/practice`로 검색한다.
7. `:%s/practice/test/g`로 전체 `practice`를 `test`로 바꾼다.
8. `gg`, `G`로 첫 줄과 마지막 줄로 이동한다.
9. `:wq`로 저장 후 종료한다.

## 2. 파일 내용 처리

```bash
head -n 5 file_content.txt
cut -d: -f6 file_content.txt > home_paths.txt
cut -d: -f7 file_content.txt | sort | uniq -c
wc file_content.txt
sed 's#/sbin/nologin#/bin/false#g' file_content.txt > modified.txt
```

`sed`에서 `#`를 구분자로 쓰면 `/sbin/nologin`처럼 `/`가 들어간 문자열을 쉽게 바꿀 수 있다.

## 3. 스크립트 작성

```bash
vi hello_user.sh
```

입력 내용:

```bash
#!/bin/bash
echo "안녕하세요, ${USER}님!"
echo "현재 날짜와 시간은:"
date
echo "현재 위치:"
pwd
```

실행:

```bash
chmod +x hello_user.sh
./hello_user.sh
```
