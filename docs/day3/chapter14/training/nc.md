# [실습] nc - 5분

1. 로컬 PC에서 `from_local`이라는 파일을 생성한 뒤, `nc` 명령어를 이용하여 해당 파일을 현재 서버의 `~/nc` 디렉터리로 복사한다.

    #### 서버에서 실행
    ```bash
    nc -l -p 12345 | tar xzf -
    ```

    ### 개인 PC 에서 실행

    ```bash
    tar czf - from_local | nc koreabio.limeops.co.kr 12345
    ```

## [답지] 답지 예시

- [답지 예시](../solution/nc_solution.md)