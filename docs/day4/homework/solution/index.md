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

conda activate py2
python --version

conda activate py3
python --version
conda deactivate
```

## 3. MySQL 실습

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

## 4. Docker 확인

```bash
docker --version
docker run --rm hello-world
```
