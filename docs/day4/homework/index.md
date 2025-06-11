## Day 4: 과제

1. 패키지 관리 도구를 이용해서 SLURM 을 다운로드 받는다. (개인 PC의 리눅스)
2. conda 를 이용해서 python 2.xx 와 3.xx 를 사용하는 환경을 만들어본다.
3. 로컬에 mysql 설치 후 아래 실습을 진행한다.
    1. mysql 에 `homework` database 를 생성한다.
    2. `homework` database 안에 `student` 라는 테이블을 생성한다. 테이블은 아래와 같은 컬럼들을 포함한다.
        1. student_id (숫자)
        2. name (문자. 10자 이 하)
        3. age (숫자)
        4. description (긴 텍스트)
    3. `student` 테이블에 아래와 같은 데이터를 입력한다.
        1. student_id : 123
        2. name: 홍길동
        3. age: 38
        4. description: 설명입니다.