## Day 3: 과제

1. GitHub에 가입한다 
- [https://github.com](https://github.com)


2. `permission` 파일을 생성하고 권한을 `rw-r--r--` 로 생성해본다.
    - 이 권한이 어떤 권한 인지도 생각해본다.

3. 아래 텍스트를 복사해서 `process.sh` 파일을 만들고 실습을 진행한다.

    ```bash
    #!/bin/bash
    for i in {1..100}; do
    echo "현재 사용자: $USER"
    sleep 60
    done
    ```
    1. 실행 권한을 부여하고 백그라운드로 실행한다.
    2. 백그라운드에서 실행 중인 `process.sh` 를 확인하고 강제 종료한다.

4. 리눅스 서버에서 만든 process.sh 파일을 scp 를 이용해서 내 로컬 컴퓨터로 이동 시킨다.