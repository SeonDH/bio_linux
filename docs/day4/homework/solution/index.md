# Day 4 과제 답지 예시

## 1. SLURM 준비

Ubuntu 계열 로컬 Linux 기준 예시이다.

```bash
sudo apt update
sudo apt install -y slurm-wlm munge
sinfo
```

설치 환경에 따라 SLURM 설정 파일 작성과 서비스 재시작이 추가로 필요할 수 있다.

## 2. conda 환경 생성

```bash
conda create -n py2 python=2.7 -y
conda create -n py3 python=3 -y
```

Python 2.x 환경 확인:

```bash
conda activate py2
python --version
```

Python 3.x 환경 확인:

```bash
conda activate py3
python --version
conda deactivate
```

실습 후 환경 삭제:

```bash
conda remove -n py2 --all -y
conda remove -n py3 --all -y
```

## 3. MySQL 따라하기

```sql
CREATE DATABASE homework;
USE homework;

CREATE TABLE student (
  student_id INT,
  name VARCHAR(10),
  age INT,
  description TEXT
);

INSERT INTO student (student_id, name, age, description)
VALUES (123, '홍길동', 38, '설명입니다.');

SELECT * FROM student;
```

## 4. Docker 설치 및 확인

Ubuntu 계열 로컬 Linux 기준 예시이다.

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable --now docker
docker --version
```

일반 사용자 계정에서 `sudo` 없이 `docker` 명령어를 쓰고 싶다면 현재 사용자를 `docker` 그룹에 추가한다.

```bash
sudo usermod -aG docker $USER
```

위 명령어를 실행한 뒤에는 터미널을 완전히 종료하고 다시 로그인해야 그룹 권한이 적용된다.
바로 확인하고 싶다면 아래처럼 `newgrp`를 사용할 수 있다.

```bash
newgrp docker
```

Docker 실행 확인:

```bash
docker --version
docker run --rm hello-world
```

만약 권한 오류가 나면 먼저 아래처럼 `sudo`를 붙여 확인할 수 있다.

```bash
sudo docker run --rm hello-world
```
