# [답지] crontab 실습

1. `do_nothing.sh` 스크립트를 매일 새벽 3시에 실행되도록 크론탭에 등록한다.

    ```bash
    crontab -e
    ```

    ```
    0 3 * * * /home/{사용자이름}/cron/do_nothing.sh
    ```

2. `file_creator.sh` 스크립트를 매분 실행되도록 등록한다.

    ```bash
    crontab -e
    ```

    ```
    * * * * * /home/{사용자이름}/cron/file_creator.sh
    ```

3. 현재 설정된 크론탭 목록을 확인한다.

    ```bash
    crontab -l
    ```

4. 등록된 크론탭을 제거한다.

    ```bash
    crontab -r
    ```
