# [답지] 계산기 만들기

## 실습 1. 사칙연산 계산기

```bash
vi calculator.sh
```

입력 내용:

```bash
#!/bin/bash

echo "첫 번째 숫자를 입력하세요:"
read num1

echo "두 번째 숫자를 입력하세요:"
read num2

echo "연산자를 입력하세요: + - * /"
read op

if [ "$op" = "+" ]; then
  echo $((num1 + num2))
elif [ "$op" = "-" ]; then
  echo $((num1 - num2))
elif [ "$op" = "*" ]; then
  echo $((num1 * num2))
elif [ "$op" = "/" ]; then
  if [ "$num2" = "0" ]; then
    echo "0으로 나눌 수 없습니다."
  else
    echo $((num1 / num2))
  fi
else
  echo "지원하지 않는 연산자입니다."
fi
```

실행:

```bash
chmod +x calculator.sh
./calculator.sh
```

## 실습 2. 구구단 출력

```bash
vi gugudan.sh
```

입력 내용:

```bash
#!/bin/bash

echo "2부터 9 사이 숫자를 입력하세요:"
read dan

for i in {1..9}; do
  echo "$dan x $i = $((dan * i))"
done
```

실행:

```bash
chmod +x gugudan.sh
./gugudan.sh
```
