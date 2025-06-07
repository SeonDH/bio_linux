# 10. 쉘 스크립트

## 쉘 스크립트란?

- **셸 스크립트**는 리눅스 셸에서 실행할 수 있는 명령어들의 모음이다.
- 반복적인 작업을 자동화하거나, 여러 명령어를 순서대로 실행할 때 사용한다.
- 작성한 명령어들은 위에서부터 한 줄씩 순차적으로 실행된다.

## 셸 스크립트의 기본 구조

1. **시작 라인 (Shebang)**: `#!/bin/bash`
2. **주석**: `#`로 시작하는 줄은 주석 처리된다.
3. **명령어**: 일반적인 쉘 명령어들을 순서대로 작성

```bash
#!/bin/bash
# 이는 첫 셸 스크립트입니다

echo "Hello, World!"
```

## 셸 스크립트 작성 및 실행 방법

1. 텍스트 편집기로 스크립트 파일 생성 (`vi`, `nano` 등 사용)

```bash
vi myscript.sh
```

2. 스크립트 작성 후 저장

```bash
#!/bin/bash
# My first shell script

echo "Hello, World!"
```

3. 실행 권한 부여

```bash
chmod +x myscript.sh
```

4. 스크립트 실행

```bash
./myscript.sh
```

## 변수 사용

### 변수란?

- 변수는 정보를 저장할 수 있는 이름표 같은 것이다. 예를 들어, 컴퓨터가 어떤 숫자나 글자를 기억하도록 하기 위해 사용한다.

- 비유: 요리할 때 설탕의 양을 종이에 적어놓고 필요할 때마다 그 종이를 참조하는 것과 같다.


```bash
#!/bin/bash

name="Alice"
echo "Hello, $name"
```

## 조건문 사용

### 조건문이란?
- 조건문은 "만약에"라는 질문을 컴퓨터에게 물어보는 것이다. 어떤 조건이 참(true)일 때와 거짓(false)일 때 다른 동작을 하게 할 수 있다.
- 비유: 비가 오면 우산을 가지고 나가고, 그렇지 않으면 선글라스를 가지고 나가는 상황과 같다.

```bash
#!/bin/bash

weather="rainy"

if [ "$weather" = "rainy" ]; then
  echo "Take an umbrella."
else
  echo "Wear sunglasses."
fi
```

## 반복문 사용

- 반복문은 어떤 작업을 여러 번 반복하게 하는 것이다. 컴퓨터에게 특정 작업을 여러 번 수행하라고 지시할 수 있다.


### for
- 비유: 친구들에게 초대장을 보내야 할 때, 한 친구에게 초대장을 보내고, 다시 또 다른 친구에게 보내는 작업을 반복하는 것과 같다.

```bash
#!/bin/bash

for i in {1..5}; do
  echo "반복문1 $i"
done

for i in 1 2 3 4 5; do
  echo "반복문2 $i"
done
```

### while

**비유**:

- 계단을 오르내릴 때 한 계단씩 올라가고, 더 이상 계단이 없을 때 멈추는 것과 같다.


```bash
#!/bin/bash

counter=1

# counter가 5 이하인 동안 반복
while [ $counter -le 5 ]
do
  echo "반복문 $counter"
  counter=$(( counter + 1 ))
done
```

## 함수 사용

- 함수는 특정 작업을 수행하는 코드의 묶음이다. 여러 번 사용할 수 있도록 이름을 붙여 놓은 코드 블록이다.
- 비유: 빵을 굽는 방법을 종이에 적어두고 필요할 때마다 그 종이를 참고하여 빵을 굽는 것과 같다.

```bash
#!/bin/bash

greet() {
  echo "Hello, $1!"
}

greet "Bob"
```

## 사칙 연산

```bash
#!/bin/bash

# 사칙 연산 함수 정의
add() {
  echo "$1 + $2 = $(( $1 + $2 ))"
}

subtract() {
  echo "$1 - $2 = $(( $1 - $2 ))"
}

multiply() {
  echo "$1 * $2 = $(( $1 * $2 ))"
}

divide() {
  if [ $2 -ne 0 ]; then
    echo "$1 / $2 = $(( $1 / $2 ))"
  else
    echo "Error: Division by zero is not allowed."
  fi
}

# 두 숫자와 연산자 지정
num1=10
num2=5

# 사칙 연산 수행
add $num1 $num2
subtract $num1 $num2
multiply $num1 $num2
divide $num1 $num2
```

## 사용자 입력 받기 (read)

```bash
#!/bin/bash

echo "이름을 입력해주세요:"
read name
echo "안녕하세요, $name 님!"
```

### -p 옵션 (bash 전용)

- read 명령어는 보통 echo와 함께 사용하지만, -p 옵션을 이용하면 한 줄로 사용자 안내 메시지와 입력을 처리할 수 있다.

```
#!/bin/bash

read -p "이름을 입력해주세요: " name
echo "안녕하세요, $name 님!"
```


## 파일 검사

```bash
#!/bin/bash

file="myfile.txt"
if [ -e "$file" ]; then
  echo "File exists"
else
  echo "File does not exist"
fi
```
- `e`: 파일이나 디렉토리가 존재하는지 검사
- `f`: 일반 파일인지 검사
- `d`: 디렉토리인지 검사
- `r`: 파일이 읽기 가능한지 검사
- `w`: 파일이 쓰기 가능한지 검사
- `x`: 파일이 실행 가능한지 검사


## 파일 읽기

```bash
#!/bin/bash

file="myfile.txt"
while IFS= read -r line; do
  echo "$line"
done < "$file"
```


## 쉘 스크립트 응용 (입력 받은 숫자 통계 내기)

```bash
#!/bin/bash
# 숫자 통계 계산 스크립트

# 변수 초기화
numbers=()
total=0

# 함수 정의
calculate_max() {
  max=${numbers[0]}
  for num in "${numbers[@]}"; do
    if [ "$num" -gt "$max" ]; then
      max=$num
    fi
  done
  echo $max
}

calculate_min() {
  min=${numbers[0]}
  for num in "${numbers[@]}"; do
    if [ "$num" -lt "$min" ]; then
      min=$num
    fi
  done
  echo $min
}

calculate_avg() {
  count=${#numbers[@]}
  avg=$(echo "$total / $count" | bc -l)
  echo $avg
}

# 숫자 입력 받기
echo "숫자를 입력하세요 (끝내려면 'done'을 입력하세요):"
while true; do
  read input
  if [ "$input" = "done" ]; then
    break
  elif [[ "$input" =~ ^[0-9]+$ ]]; then
    numbers+=($input)
    total=$((total + input))
  else
    echo "유효한 숫자를 입력하세요."
  fi
done

# 입력된 숫자가 없는 경우
if [ ${#numbers[@]} -eq 0 ]; then
  echo "입력된 숫자가 없습니다."
  exit 1
fi

# 최대값, 최소값, 평균 계산 및 출력
max=$(calculate_max)
min=$(calculate_min)
avg=$(calculate_avg)

echo "입력된 숫자들: ${numbers[@]}"
echo "최대값: $max"
echo "최소값: $min"
echo "평균: $avg"
```



## [실습] 계산기 만들기 - 20분

[[실습] 계산기 만들기](training/calculater.md)


# 포그라운드와 백그라운드 작업

리눅스에서는 명령어를 **포그라운드(기본)** 또는 **백그라운드**에서 실행할 수 있다.

### 포그라운드 작업

- 사용자가 명령어를 입력하고, 해당 작업이 끝날 때까지 터미널을 점유하는 방식
- 예: `sleep 10` 을 실행하면 10초 동안 터미널이 잠김

```bash
sleep 10       # 포그라운드 실행
```

### 백그라운드 작업

- 명령어 끝에 `&`를 붙이면 터미널을 점유하지 않고 백그라운드에서 실행됨

```bash
sleep 10 &     # 백그라운드 실행
```

### 작업 제어 명령어

```bash
jobs            # 백그라운드 작업 목록 보기
fg %1           # 첫 번째 작업 포그라운드로 이동
bg %1           # 첫 번째 작업 백그라운드로 재시작
kill %1         # 첫 번째 작업 종료
```

- `Ctrl + Z`: 현재 작업을 일시 정지 상태로 보냄
- `Ctrl + C`: 현재 작업을 강제 종료

[[실습] 포그라운드 백그라운드 - 5분](training/fgbg.md)

## nohup 사용

- 사용자가 로그아웃해도 백그라운드 작업을 유지

```bash
nohup ./script.sh > output.log 2>&1 &
```

[[실습] nohup - 5분](training/nohup.md)

## watch 사용

- 주기적으로 명령어를 실행하고 결과를 갱신

```bash
watch -n 1 date
watch -n 1 ./myscript.sh
```

- 명령어 치환을 활용하면 동적인 결과를 출력할 수 있음

```bash
#!/bin/bash
echo "현재 시각은 $(date)"
```

## 명령어 치환

[[번외] 명령어 치환](extra/command.md) — `$(command)` 또는 백틱(``)을 사용하여 명령어의 실행 결과를 문자열에 삽입할 수 있다.

## 디버깅 팁

스크립트 상단에 `set -e` 를 추가하여 디버깅 정보 출력

```bash
#!/bin/bash

set -e
trap 'echo "오류: 줄 번호 $LINENO, 오류 코드: $?"' ERR
```

### 디버그 실행

- x 옵션을 사용하여 스크립트의 각 명령어가 실행될 때 출력되도록 한다.

```bash
bash -x script.sh
```

[[번외] bash 로 실행과 ./ 로 실행 차이](extra/execute.md)

## 요약

1. 쉘 스크립트는 순차적으로 명령어를 실행한다.
2. 실행 권한을 부여하고 `./`로 실행한다.
3. 백그라운드 실행, `nohup`, `watch`는 자동화 작업에 유용하다.
4. 디버깅을 위해 `set -e`와 `trap`을 활용할 수 있다.
5. `$(명령어)` 또는 ``명령어``를 통해 명령어 실행 결과를 문자열에 삽입할 수 있다.