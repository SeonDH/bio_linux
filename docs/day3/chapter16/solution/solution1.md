# [답지] 스크립트 1

- 답지의 예시일 뿐이며 여러 답지도 가능하다.

```bash
# 1. Hello World
echo "Hello, World!"

# 2. 변수 사용
name="YourName"
echo "Hello, $name"

# 3. 파일 존재 여부 확인
file="yourfile.txt"
if [ -e "$file" ]; then
  echo "File exists"
else
  echo "File does not exist"
fi

# 4. 파일 읽기
file="yourfile.txt"
while IFS= read -r line; do
  echo "$line"
done < "$file"

# 5. 조건문 사용
number=15
if [ "$number" -gt 10 ]; then
  echo "Greater than 10"
else
  echo "10 or less"
fi

# 6. 반복문 사용
for i in {1..10}; do
  echo "$i"
done

# 7. 사용자 입력 받기
read -p "Enter your name: " name
echo "Hello, $name"

# 8. 현재 날짜 출력
date

# 9. 파일 크기 확인
file="yourfile.txt"
if [ -e "$file" ]; then
  stat -c%s "$file"
else
  echo "File does not exist"
fi

# 10. 디렉토리 리스트
ls -l
```