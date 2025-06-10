---
title: "16. 쉘 스크립트 고급"
nav_order: 22
layout: default
---


# 16. [실습] 쉘 스크립트 고급

아래 조건을 작성만족하는 스크립트를 작성한다.
    - 파일에 대한 스크립트는 임의의 파일 이름(ex: yourfile.txt) 이 있다고 가능
    - 디렉터리에 대한 스크립트도 임의의 디렉터리(ex: yourdir)가 존재한다고 가정한다.

> 목적: 모든 스크립트가 반드시 동작할 필요는 없으며, 어떤 명령어를 어떻게 구성해야 할지 감을 잡는 것이 목표이다.

## 15분 실습

1. **Hello World**: "Hello, World!"를 출력하시오.
2. **변수 사용**: 변수 `name`에 본인의 이름을 저장하고, "Hello, [name]"을 출력하시오.
3. **파일 존재 여부 확인**: 특정 파일이 존재하면 "File exists", 아니면 "File does not exist"를 출력하시오.
4. **파일 읽기**: 텍스트 파일의 내용을 출력출력하시오.
5. **조건문 사용**: 숫자 변수의 값이 10보다 크면 "Greater than 10", 아니면 "10 or less"를 출력하시오.
6. **반복문 사용**: 1부터 10까지 숫자를 출력하시오.
7. **사용자 입력 받기**: 이름을 입력 받아 "Hello, [name]"을 출력하시오.
8. **현재 날짜 출력**: 현재 날짜와 시간을 출력하시오.
9. **파일 크기 확인**: 특정 파일의 크기를 출력하시오.
10. **디렉토리 리스트**: 현재 디렉토리의 파일과 디렉토리를 출력하시오.

### 답지 예시 1
- [답지 예시 1](solution/solution1.md)


## 15분 실습

1. **숫자 더하기**: 두 숫자를 입력받아 합을 출력하시오.
2. **단어 수 세기**: 텍스트 파일에서 단어 수를 세어 출력하시오.
3. **파일 복사**: 특정 파일을 다른 위치로 복사하시오.
4. **환경 변수 출력**: 환경 변수명을 입력받아 값을 출력하시오.
5. **문자열 길이**: 문자열을 입력받아 길이를 출력하시오.
6. **기본 계산기**: 숫자, 연산자, 숫자를 입력받아 연산 결과를 출력하시오. (`+`, `-`, `*`, `/` 지원)
7. **문자열 포함 여부**: 문자열과 단어를 입력받아 포함 여부를 확인하시오.
8. **프로세스 리스트**: 현재 실행 중인 프로세스를 출력하시오.

### 답지 예시 2
- [답지 예시 2](solution/solution2.md)

## 15분 실습

1. **파일 정렬**: 텍스트 파일 내용을 정렬하여 출력하시오.
2. **파일 압축**: 특정 디렉토리의 파일을 압축하시오.
    - `tar` 명령어 참고
3. **파일 권한 변경**: 특정 파일의 권한을 변경하시오.
4. **문자열 치환**: 파일 내 특정 문자열을 다른 문자열로 치환하시오.
5. **프로세스 상태 체크**: 특정 프로세스가 실행 중인지 확인하고, 아니면 실행하도록 하시오.
6. **IP 주소 확인**: 현재 시스템의 IP 주소를 출력하시오.
    - `ip` 명령어 참고
7. **로그 감시**: 로그 파일을 모니터링하여 특정 단어가 나오면 메시지를 출력하시오.

### 답지 예시 3
- [답지 예시 3](solution/solution3.md)

## 10분 실습 — 스크립트 해석 문제

다음 스크립트는 각각 무엇을 하는가? 간략히 설명하시오.

1.

```bash
#!/bin/bash
for file in *.log; do
    echo "Analyzing $file ..."
    grep "ERROR" $file > errors.txt
done
```

2.

```bash
#!/bin/bash
total=0
for num in 1 2 3 4 5; do
    ((total += num))
done
echo "Total sum is: $total"
```

3. cat /etc/passwd 가 어느 파일인지 확인해본다.

```bash
#!/bin/bash
for user in $(awk -F':' '{ print $1 }' /etc/passwd); do
    echo "User: $user"
done
```

4.

```bash
#!/bin/bash
if [ ! -d "/backup" ]; then
    mkdir /backup
fi
tar czf /backup/home_backup_$(date +%Y%m%d).tar.gz /home
```

5.

```bash
#!/bin/bash
function greet {
    echo "Hello, $1!"
}
greet "Alice"
```

6.

```bash
#!/bin/bash
for process in $(ps aux | grep "java" | awk '{ print $2 }'); do
    echo "Killing process: $process"
    kill -9 $process
done
```

7.

```bash
#!/bin/bash
if [ -z "$1" ]; then
    echo "No arguments supplied."
    exit 1
fi
echo "Processing file: $1"
```

8.

```bash
#!/bin/bash
function fibonacci {
    if [ $1 -eq 0 ]; then
        echo 0
    elif [ $1 -eq 1 ]; then
        echo 1
    else
        echo $(( $(fibonacci $(( $1 - 1 ))) + $(fibonacci $(( $1 - 2 ))) ))
    fi
}

result=$(fibonacci 6)
echo "Fibonacci sequence at position 6 is: $result"
```

9.

```bash
#!/bin/bash
for file in $(find /var/log -name "*.log"); do
    echo "Compressing $file ..."
    gzip $file
done
```

10.

```bash
#!/bin/bash
echo "Welcome to the script!"
echo "Current date and time: $(date)"
echo "Running processes:"
ps -ef
```

### 답지 예시 4
- [답지 예시 4](solution/solution4.md)