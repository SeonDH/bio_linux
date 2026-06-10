## Day 4: 과제

1. Day 5 SLURM 실습 준비
    - 로컬 Linux 환경에서 패키지 관리 도구를 이용해 SLURM 관련 구성 요소를 설치하고, 단일 노드 실습용으로 동작을 확인한다.
2. conda 를 이용해서 Python 2.x 와 3.x 를 사용하는 환경을 만들어보고, 환경별로 실행 버전이 달라짐을 확인한다.
3. MySQL은 중요도가 높지 않으므로, 로컬 Linux에서 예제를 보고 따라 실행하며 기본 구조만 확인한다.
    - 아래 내용은 정답을 외우기 위한 과제가 아니라, database, table, row, column 개념을 확인하기 위한 따라하기 실습이다.
    1. mysql 에 `homework` database 를 생성한다.
    2. `homework` database 안에 `student` 라는 테이블을 생성한다. 테이블은 아래와 같은 컬럼들을 포함한다.
        1. student_id (숫자)
        2. name (문자. 10자 이하)
        3. age (숫자)
        4. description (긴 텍스트)
    3. `student` 테이블에 아래와 같은 데이터를 입력한다.
        1. student_id : 123
        2. name: 홍길동
        3. age: 38
        4. description: 설명입니다.

4. Day 5 Docker 실습 준비
    - 로컬 Linux에 Docker를 설치한다.
    - 설치 후 아래 명령어가 실행되는지 확인한다.

    ```bash
    docker --version
    docker run --rm hello-world
    ```

    - 로컬 Linux 터미널에서 위 명령어를 실행해 확인한다.

## 답지

- [답지 예시](solution/index.md)
