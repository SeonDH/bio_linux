# [답지] rsync

## 명령어 (원격 접속을 하지 않고 내 개인 PC 에서 날려야한다)

1. 로컬 PC에 `from_local1` 파일을 생성한다.
    ```
    cd ~/rsync
    touch from_local1
    ```

2. 다음 명령어를 이용하여 원격 서버와 디렉터리를 동기화한다. (동기화 후 서버의 파일 상태 확인)
    ```bash
    rsync -e 'ssh -p 1119 -o Ciphers=aes256-cbc' -avz ./from_local user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/rsync
    ```

3. 로컬 PC에 `from_local2` 파일을 추가로 생성한다.
    ```
    cd ~/rsync
    touch from_local2
    ```

4. 다시 위의 `rsync` 명령어를 사용하여 디렉터리를 동기화한다. (동기화 후 서버의 파일 상태 확인)
    ```bash
    rsync -e 'ssh -p 1119 -o Ciphers=aes256-cbc' -avz ./from_local user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/rsync
    ```