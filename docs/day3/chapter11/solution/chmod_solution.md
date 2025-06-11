# [답지] 파일 권한 변경

- 답지의 예시일 뿐이며 여러 답지도 가능하다.

1. 기본 파일 권한 확인
    ```
    ls -l hello.sh
    ```

2. 권한 부족으로 "Permission denied"

    ```
    ./hello.sh
    ```

3. 소유자에게 실행 권한 추가
    ```
    chmod u+x hello.sh
    ```

4. 정상 출력
    ```
    "Hello, World!"
    ```