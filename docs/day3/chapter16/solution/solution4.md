# [답지] 스크립트 4

1. 로그 파일에서 ERROR 추출

    - 현재 디렉토리의 .log 파일들을 순회하며 "ERROR"가 포함된 내용을 errors.txt에 매번 덮어쓰기함.

    ```bash
    for file in *.log; do
        echo "Analyzing $file ..."
        grep "ERROR" $file > errors.txt
    done
    ```

2. 숫자 합계 계산

    - 1부터 5까지의 수를 더해서 합계를 출력함.


    ```bash
    total=0
    for num in 1 2 3 4 5; do
        ((total += num))
    done
    echo "Total sum is: $total"
    ```


3. 사용자 이름 출력

    - 시스템에 등록된 모든 사용자 계정 이름을 출력함.


    ```bash
    for user in $(awk -F':' '{ print $1 }' /etc/passwd); do
        echo "User: $user"
    done
    ```


4. 홈 디렉토리 백업

    - /backup 디렉토리가 없으면 생성하고, /home 디렉토리를 날짜 형식으로 압축하여 백업함.

    ```bash
    if [ ! -d "/backup" ]; then
        mkdir /backup
    fi
    tar czf /backup/home_backup_$(date +%Y%m%d).tar.gz /home
    ```
    

5. 함수로 인사 메시지 출력

    - greet 함수로 "Hello, Alice!" 인사말을 출력함.

    ```bash
    function greet {
        echo "Hello, $1!"
    }
    greet "Alice"
    ```

6. java 프로세스 강제 종료

    - java라는 이름이 포함된 프로세스의 PID를 찾아 kill -9으로 강제 종료함

    ```bash
    for process in $(ps aux | grep "java" | awk '{ print $2 }'); do
        echo "Killing process: $process"
        kill -9 $process
    done
    ```


7. 인자 유무 검사

    - 인자($1)가 없으면 경고 메시지를 출력하고 종료, 있으면 해당 인자를 파일로 처리함.

    ```bash
    if [ -z "$1" ]; then
        echo "No arguments supplied."
        exit 1
    fi
    echo "Processing file: $1"
    ```



8. 재귀적으로 피보나치 수 계산
    - 재귀 함수를 이용해 피보나치 수열의 6번째 값을 계산함.
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

9. 로그 파일 압축
    - /var/log 아래의 .log 파일을 찾아 하나씩 gzip으로 압축함.
    ```bash
    #!/bin/bash
    for file in $(find /var/log -name "*.log"); do
        echo "Compressing $file ..."
        gzip $file
    done
    ```


10. 환영 메시지와 시스템 정보 출력
    - 스크립트 실행 시 현재 시간과 실행 중인 프로세스를 보여줌.
    ```bash
    echo "Welcome to the script!"
    echo "Current date and time: $(date)"
    echo "Running processes:"
    ps -ef
    ```

