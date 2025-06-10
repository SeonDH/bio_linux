# [답지] 스크립트 3

- 답자의 예시일 뿐이며 여러 답안도 가능하다.

```bash
# 1. 파일 정렬
file="yourfile.txt"
if [ -e "$file" ]; then
  sort "$file"
else
  echo "File does not exist"
fi

# 2. 파일 압축
dir="yourdir"
tar -czvf backup.tar.gz "$dir"


# 3. 파일 권한 변경
file="yourfile.txt"
chmod 644 "$file"


# 5. 문자열 치환
file="yourfile.txt"
sed -i 's/oldstring/newstring/g' "$file"


# 6. 프로세스 상태 체크 및 실행
process="yourprocess"
if ps -ef | grep "$process" > /dev/null; then
  echo "$process is running"
else
  echo "$process is not running"
  "$process" &
fi


# 7. IP 주소 확인
ip addr | grep 'inet ' | grep -v '127.0.0.1' | awk '{print $2}' | cut -d/ -f1


# 8. 로그 파일에서 특정 단어 감시
file="yourlogfile.log"
word="ERROR"
tail -f "$file" | while read line; do
  if [[ "$line" == *"$word"* ]]; then
    echo "$word found: $line"
  fi
done
```