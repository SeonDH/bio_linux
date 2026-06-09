# [답지] rsync

## 명령어

아래 명령은 원격 서버에 접속한 상태가 아니라, 내 개인 PC 터미널에서 실행한다.
`user31`은 예시 계정이므로 본인에게 배정된 계정과 경로로 바꿔서 사용한다.

1. 로컬 PC에 `from_local1` 파일을 생성한다.

    ```bash
    cd ~/rsync
    touch from_local1
    ```

2. 다음 명령어를 이용하여 원격 서버와 디렉터리를 동기화한다. (동기화 후 서버의 파일 상태 확인)

    ```bash
    rsync -e 'ssh -p 1119 -o Ciphers=aes256-cbc' -avz ~/rsync/ user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/rsync/
    ```

3. 로컬 PC에 `from_local2` 파일을 추가로 생성한다.

    ```bash
    cd ~/rsync
    touch from_local2
    ```

4. 다시 위의 `rsync` 명령어를 사용하여 디렉터리를 동기화한다. (동기화 후 서버의 파일 상태 확인)

    ```bash
    rsync -e 'ssh -p 1119 -o Ciphers=aes256-cbc' -avz ~/rsync/ user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/rsync/
    ```
