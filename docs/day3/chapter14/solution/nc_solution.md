


## [답지] nc

1. 로컬 PC에서 `from_local`이라는 파일을 생성한 뒤, `nc` 명령어를 이용하여 해당 파일을 현재 서버의 `~/nc` 디렉터리로 복사한다.

    서버에서 먼저 수신 대기:

    ```bash
    mkdir -p ~/nc
    cd ~/nc
    nc -l -p 12345 | tar xzf -
    ```

    개인 PC에서 파일 전송:

    ```bash
    cd ~/nc
    touch from_local
    tar czf - from_local | nc koreabio.limeops.co.kr 12345
    ```
