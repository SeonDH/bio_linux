# [실습] nc - 5분

> 선택 실습: 포트 개념을 확인하기 위한 실습이다. 일반적인 파일 전송은 `scp` 또는 `rsync`를 우선 사용한다.

1. 로컬 PC에서 `from_local`이라는 파일을 생성한 뒤, `nc` 명령어를 이용하여 해당 파일을 현재 서버의 `~/nc` 디렉터리로 복사한다.

    #### 서버에서 실행

    ```bash
    mkdir -p ~/nc
    cd ~/nc
    ```

    ```bash
    nc -l -p 12345 | tar xzf -
    ```

    ### 개인 PC에서 실행

    ```bash
    tar czf - from_local | nc koreabio.limeops.co.kr 12345
    ```

## [답지] 답지 예시

- [답지 예시](../solution/nc_solution.md)
