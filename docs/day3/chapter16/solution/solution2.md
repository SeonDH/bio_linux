# [답지] 스크립트 2

- 답지의 예시일 뿐이며 여러 답지도 가능하다.

```bash
# 1. 숫자 더하기
read -p "Enter first number: " num1
read -p "Enter second number: " num2
sum=$((num1 + num2))
echo "Sum: $sum"

# 2. 단어 수 세기
file="yourfile.txt"
if [ -e "$file" ]; then
  wc -w "$file"
else
  echo "File does not exist"
fi

# 3. 파일 복사
src="yourfile.txt"
dst="backupfile.txt"
cp "$src" "$dst"

# 4. 환경 변수 출력
read -p "Enter the name of the environment variable: " var_name
echo "${!var_name}"

# 5. 문자열 길이
read -p "Enter a string: " str
echo "Length of the string is: ${#str}"

# 6. 기본 계산기
read -p "Enter first number: " num1
read -p "Enter operator (+ - * /): " op
read -p "Enter second number: " num2

case "$op" in
  +) result=$((num1 + num2)) ;;
  -) result=$((num1 - num2)) ;;
  \*) result=$((num1 * num2)) ;;
  /) result=$((num1 / num2)) ;;
  *) echo "Invalid operator"; exit 1 ;;
esac

echo "Result: $result"

# 7. 문자열 포함 여부
read -p "Enter the main string: " str
read -p "Enter the substring to search for: " sub
if [[ "$str" == *"$sub"* ]]; then
  echo "String contains $sub"
else
  echo "String does not contain $sub"
fi

# 8. 프로세스 리스트
ps aux
```