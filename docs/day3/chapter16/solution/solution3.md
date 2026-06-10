# [답지] 스크립트 3

- 답지의 예시일 뿐이며 여러 답지도 가능하다.

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


# 4. 문자열 치환
file="yourfile.txt"
sed -i 's/oldstring/newstring/g' "$file"


# 5. 프로세스 상태 체크 및 실행
process="yourprocess"
if pgrep -f "$process" > /dev/null; then
  echo "$process is running"
else
  echo "$process is not running"
  "$process" &
fi


# 6. IP 주소 확인
ip addr show


# 7. 로그 파일에서 특정 단어 감시
file="yourlogfile.log"
word="ERROR"
timeout 30s tail -f "$file" | grep "$word"
```
