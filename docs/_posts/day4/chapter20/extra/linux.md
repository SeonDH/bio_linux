# [번외] 리눅스 MySQL 띄워보기

# MySQL 설치 및 실행

### 1. 시스템 업데이트

먼저 시스템 패키지 목록을 업데이트한다.

```
sudo apt update
```

### 2. MySQL 서버 설치

`apt-get` 명령어를 사용하여 MySQL 서버 패키지를 설치한다.

```
sudo apt install mysql-server
```

### 3. MySQL 서버 시작

MySQL 서버를 시작한다.

```
sudo systemctl start mysql
```

### 4. MySQL 서버 상태 확인

MySQL 서버가 제대로 실행되고 있는지 확인한다.

```
sudo systemctl status mysql
```

### 5. MySQL 접속

MySQL 클라이언트를 사용하여 MySQL 서버에 접속한다.

```
sudo mysql -u root -p
```

- `u` 옵션은 사용자명을 지정하고, `p` 옵션은 비밀번호 입력을 요청한다.
- 명령어를 실행하고 비밀번호 입력

### 7. MySQL 기본 명령어

MySQL 클라이언트에 접속한 후 몇 가지 기본 명령어를 사용하여 데이터베이스와 테이블을 생성하고 데이터를 삽입할 수 있다.

### 데이터베이스 생성

```sql
CREATE DATABASE mydatabase;
```

### 데이터베이스 사용

```sql
USE mydatabase;
```

### 테이블 생성

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

### 데이터 삽입

```sql
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```

### 데이터 조회

```sql
SELECT * FROM users;
```

### 8. MySQL 종료

MySQL 클라이언트를 종료하려면 다음 명령어를 입력한다.

```sql
EXIT;
```