# [번외] 리눅스 MySQL 띄워보기

# MySQL 설치 및 실행

### 1. 시스템 업데이트

먼저 시스템 패키지 목록을 업데이트한다.

```shell
sudo apt update
```

### 2. MySQL 서버 설치

`apt-get` 명령어를 사용하여 MySQL 서버 패키지를 설치한다.

```shell
sudo apt install mysql-server
```

### 3. MySQL 서버 시작

MySQL 서버를 시작한다.

```shell
sudo systemctl start mysql
```

### 4. MySQL 서버 상태 확인

MySQL 서버가 제대로 실행되고 있는지 확인한다.

```shell
sudo systemctl status mysql
```

### 5. MySQL 접속

MySQL 클라이언트를 사용하여 MySQL 서버에 접속한다.
 - 기본 세팅으로 접근
```shell
sudo mysql -u root
```