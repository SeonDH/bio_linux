## Day 2: 과제



1. 아래 텍스트를 복사해서 `vi_practice.txt` 파일을 만들고 실습을 진행한다.

    ```
    Line 1: This is a simple text file used to practice vi editor commands.
    Line 2: Each line in this file has a line number at the beginning.
    Line 3: You can use this file to try movement commands like h, j, k, l.
    Line 4: Try deleting this line using the dd command.
    Line 5: This line should be copied and pasted below using yy and p.
    Line 6: Try replacing a word in this line using the r or cw command.
    Line 7: You can also try searching for a word like 'practice' using /practice.
    Line 8: Undo your last change using u, or redo using Ctrl + r.
    Line 9: Move to the start (gg) or end (G) of the file.
    Line 10: Save your file with :w and quit with :q
    ```

    1. Line 1 아래에 Line one 의 내용을 그대로 타이핑 해본다.

    2. Line 6,7 을 한번에 삭제한다.

    3. 마지막으로 작업한 Line 6,7 삭제 작업을 취소한다.

    4. Line 5 를 복사해서 Line 8 밑으로 복사한다.

    5. 6번째 줄에서 라인을 line -> LINE 으로 수정해본다.

    6. practice 를 검색해본다.

    7. 전체 practice 를 한번에 test 로 변경해본다.

    8. 첫줄, 마지막 줄로 이동해본다.

    9. 저장 후 종료 해본다.

2. 아래 텍스트를 복사해서 file_content.txt 파일을 만들고 실습을 진행한다.

    ```
    user1:x:1000:1000:User One:/home/user1:/bin/bash
    user2:x:1001:1001:User Two:/home/user2:/bin/bash
    user3:x:1002:1002:User Three:/home/user3:/sbin/nologin
    user4:x:1003:1003:User Four:/home/user4:/bin/zsh
    user5:x:1004:1004:User Five:/home/user5:/bin/bash
    user6:x:1005:1005:User Six:/home/user6:/bin/false
    user7:x:1006:1006:User Seven:/home/user7:/bin/bash
    user8:x:1007:1007:User Eight:/home/user8:/usr/sbin/nologin
    ```

    1. file_content.txt의 처음 5줄을 head 명령어로 출력해본다.

    2. 모든 사용자들의 홈 디렉터리 경로만 추출해서 home_paths.txt에 저장
        - /home/user1 같은 경로만 남기기

    3. 사용자 셸 종류의 종류별로 몇 명인지 확인
        - /bin/bash, /bin/zsh 별로 몇명 씩인지 분류

    4. 파일 전체 줄 수, 단어 수, 문자 수를 출력해본다.

    5. 파일 내의 /sbin/nologin을 모두 /bin/false로 바꿔서 modified.txt에 저장한다.


3. 아래 요구사항에 맞는 스크립트를 작성한다:

    - 파일명: hello_user.sh

    - 수행 내용:

        - 현재 사용자의 이름을 출력한다 (hint: $USER)

        - 현재 날짜와 시간을 출력한다 (hint: date)

        - 현재 작업 중인 디렉토리 경로를 출력한다 (hint: pwd)

    - 작성 후 실행 권한을 부여하고 실행한다.

    - 예시 출력
        ```
        안녕하세요, user31님!
        현재 날짜와 시간은: 2025년 06월 08일 14:35:12 입니다.
        현재 위치: /home/user31/day2/chapter10
        ```
