# [답지] ps 실습

- 답자의 예시일 뿐이며 여러 답안도 가능하다.

1. 실행 중인 프로세스 목록에서 `sleep_script.sh` 프로세스를 확인한다.

    ```bash
    $ ps -ef | grep sleep_script.sh | grep -v grep
    ```


2. 해당 프로세스를 종료한다.

    ```bash
    $ kill {pid} 
    ```

    or 

    ```bash
    $ pkill -f sleep_script.sh
    ```