# [답지] crontab 실습

1. `do_nothing.sh` 스크립트를 매일 새벽 3시에 실행되도록 크론탭에 등록한다.
    crontab -e
    ```
    0 3 * * * /{path}/do_nothing.sh
    ```

2. `file_creater.sh` 스크립트를 매분 실행되도록 등록한다.
    crontab -e
    ```
    * * * * * file_creater.sh
    ```

3. 현재 설정된 크론탭 목록을 확인한다.
    ```
    crontab -l
    ```

4. 등록된 크롭탭을 제거한다.
    ```
    crontab -r
    ```