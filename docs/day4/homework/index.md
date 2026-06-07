## Day 4: 과제

1. Day 5 SLURM 실습 준비
    - 개인 PC의 리눅스 환경에서 패키지 관리 도구를 이용해 SLURM 관련 구성 요소를 설치하고, 단일 노드 실습용으로 동작을 확인한다.
2. conda 를 이용해서 Python 2.x 와 3.x 를 사용하는 환경을 만들어보고, 환경별로 실행 버전이 달라짐을 확인한다.
3. 로컬에 mysql 설치 후 아래 실습을 진행한다.
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
    - 개인 로컬 PC에 Docker를 설치한다.
    - 설치 후 아래 명령어가 실행되는지 확인한다.

    ```bash
    docker --version
    docker run --rm hello-world
    ```

    - macOS: Docker Desktop을 설치한 뒤 터미널에서 확인한다.
    - Windows: Docker Desktop for Windows와 MobaXterm을 설치한 뒤, MobaXterm의 터미널에서 확인한다.
