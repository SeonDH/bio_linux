---
title: "20. MySQL 실습 기초"
nav_order: 26
layout: default
---


# 20. MySQL 실습 기초

## 데이터베이스란?

* 데이터를 체계적으로 저장하고 관리하는 시스템
* 효율적인 검색, 수정, 삭제가 가능하며 무결성과 일관성을 유지함
* 여러 사용자와 애플리케이션이 동시에 접근 가능
* 일반 파일 저장보다 구조화된 방식으로 데이터를 활용할 수 있음


## MySQL 개요

* 세계적으로 널리 사용되는 오픈 소스 관계형 데이터베이스 관리 시스템(RDBMS)
* 오라클이 관리하며, 무료와 유료 버전 모두 존재함

### 관계형 데이터베이스(RDB)

* 데이터를 테이블 형태로 저장하며, 테이블 간 관계를 설정함
* SQL을 사용하여 데이터 정의, 조작, 제어 가능
* ACID 속성을 만족하여 트랜잭션 처리에 적합함


## 데이터 구조

* **Database**: 여러 테이블을 포함하는 최상위 단위
* **Table**: 행(Row)과 열(Column)로 구성
* **Row**: 데이터 레코드
* **Column**: 데이터 속성, 특정 타입 가짐
    - 예: 고객 정보를 저장하는 `customers` 테이블은 ID, 이름, 이메일 컬럼 포함


## [번외] 리눅스에서 MySQL 띄우기

* [[번외] 리눅스에서 MySQL 띄우기](extra/linux.md)

## [번외] mysql 로컬 설치

- [[번외] mysql 로컬 설치](extra/local.md)


## 데이터베이스 생성 및 삭제

```sql
CREATE DATABASE database_name; --데이터베이스 생성
DROP DATABASE database_name;   --데이터베이스 삭제
```

## [실습] 데이터베이스 생성

```sql
CREATE DATABASE library;
```

## 테이블 생성, 수정 및 삭제

```sql
-- 테이블 생성
CREATE TABLE table_name (
  column1 datatype,
  column2 datatype,
  ...
); 

-- 테이블 수정
ALTER TABLE table_name ADD column_name datatype; 

-- 테이블 삭제
DROP TABLE table_name; 
```


## 테이블 생성 및 관리

### [실습] 테이블 생성

```sql
-- 데이터베이스 사용
USE library;

-- authors 테이블 생성
CREATE TABLE authors (
    author_id INT AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    birthdate DATE,
    PRIMARY KEY (author_id)
);

-- books 테이블 생성
CREATE TABLE books (
    book_id INT AUTO_INCREMENT,
    title VARCHAR(200) NOT NULL,
    author_id INT,
    publication_date DATE,
    price DECIMAL(10, 2),
    PRIMARY KEY (book_id),
    FOREIGN KEY (author_id) REFERENCES authors(author_id)
);
```

### 데이터 타입의 이해 (INT, VARCHAR, DATE)

- **INT**: 정수형 데이터 타입.
- **VARCHAR**: 가변 길이 문자열 데이터 타입.
- **DATE**: 날짜 데이터 타입 (YYYY-MM-DD).
- DECIMAL(10, 2): 최대 8자리의 정수 부분과 2자리의 소수 부분 숫자

### 기본 키와 외래 키 개념

- **기본 키 (Primary Key)**: 각 행을 고유하게 식별하는 컬럼. 중복 값을 가질 수 없고, NULL 값을 허용하지 않음.
- **외래 키 (Foreign Key)**: 다른 테이블의 기본 키를 참조하는 컬럼. 테이블 간의 관계를 정의.

## 데이터 삽입

```
-- 데이터 삽입
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```

## [실습] 데이터 삽입

```sql
-- authors 데이터 삽입
INSERT INTO authors (name, birthdate) VALUES
('J.K. Rowling', '1965-07-31'),
('George R.R. Martin', '1948-09-20');

-- books 데이터 삽입
INSERT INTO books (title, author_id, publication_date, price) VALUES
('Harry Potter and the Sorcerer''s Stone', 1, '1997-06-26', 19.99),
('A Game of Thrones', 2, '1996-08-06', 29.99);
```


## 데이터 조회

```sql
-- 전체 조회
SELECT column1, column2 FROM table_name;
-- 조건 만족하는 행만 조회
SELECT column1, column2 FROM table_name WHERE condition;
-- 중복된 값을 제거
SELECT DISTINCT column1 FROM table_name;
-- 결과를 정렬해서 조회
SELECT column1, column2 FROM table_name ORDER BY column1 [ASC|DESC];
```

## [실습] 데이터 조회


```sql
-- 모든 책 조회
SELECT * FROM books;

-- 특정 작가의 책 조회 (WHERE 절 사용)
SELECT * FROM books WHERE author_id = 1;

-- 중복 제거된 작가 이름 조회 (DISTINCT 사용)
SELECT DISTINCT name FROM authors;

-- 책 제목을 오름차순으로 정렬 (ORDER BY 사용)
SELECT title FROM books ORDER BY title ASC;
```

## 데이터 수정 및 삭제

```sql
-- 데이터 수정
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
-- 데이터 삭제
DELETE FROM table_name WHERE condition;
```

## [실습] 데이터 수정 및 삭제

```sql
-- 책 가격 업데이트
UPDATE books SET price = 18.99 WHERE title = 'Harry Potter and the Sorcerer''s Stone';

-- 책 삭제
DELETE FROM books WHERE title = 'A Game of Thrones';
```


## 조건문 및 연산자

```sql
-- AND, OR, NOT
SELECT * FROM books WHERE price > 15 AND publication_date < '2000-01-01';

-- LIKE
SELECT * FROM books WHERE title LIKE 'Harry%';

-- BETWEEN
SELECT * FROM books WHERE price BETWEEN 10 AND 30;

-- IN
SELECT * FROM authors WHERE name IN ('J.K. Rowling', 'George R.R. Martin');

-- IS NULL
SELECT * FROM authors WHERE birthdate IS NULL;
```

## [실습] 조건문으로 조회

```sql
-- 특정 가격 범위 내의 책 조회 (BETWEEN 사용)
SELECT * FROM books WHERE price BETWEEN 15 AND 20;

-- 여러 조건을 만족하는 책 조회 (AND 사용)
SELECT * FROM books WHERE price > 15 AND publication_date < '2000-01-01';

-- NULL 값을 가진 작가 조회 (IS NULL 사용)
SELECT * FROM authors WHERE birthdate IS NULL;
```


## 함수 사용

```sql
-- 문자열 함수
SELECT CONCAT('Author: ', name) FROM authors;
SELECT LENGTH(name) FROM authors;

-- 수치 함수
SELECT ROUND(price, 0) FROM books;
SELECT CEIL(price) FROM books;
SELECT FLOOR(price) FROM books;

-- 날짜 함수
SELECT NOW();
SELECT CURDATE();
SELECT DATE_FORMAT(publication_date, '%Y-%m-%d') FROM books;

-- 집계 함수
SELECT COUNT(*) FROM books;
SELECT SUM(price) FROM books;
SELECT AVG(price) FROM books;
SELECT MAX(price) FROM books;
SELECT MIN(price) FROM books;
```

## [실습] 함수 사용

```sql
-- 책 제목 결합 (CONCAT 사용)
SELECT CONCAT('Title: ', title) FROM books;

-- 작가 이름의 길이 반환 (LENGTH 사용)
SELECT name, LENGTH(name) AS name_length FROM authors;

-- 책 가격의 평균 계산 (AVG 사용)
SELECT AVG(price) AS average_price FROM books;

-- 현재 날짜와 시간 조회 (NOW 사용)
SELECT NOW();
```

## 조인

### NNER JOIN: 두 테이블 간의 조인

- **INNER JOIN**: 두 테이블에서 일치하는 행을 반환.
    
    ```sql
    SELECT table1.column1, table2.column2
    FROM table1
    INNER JOIN table2 ON table1.common_column = table2.common_column;
    ```
    

### LEFT JOIN: 왼쪽 테이블을 기준으로 한 조인

- **LEFT JOIN**: 왼쪽 테이블의 모든 행과 오른쪽 테이블에서 일치하는 행을 반환.
    
    ```sql
    SELECT table1.column1, table2.column2
    FROM table1
    LEFT JOIN table2 ON table1.common_column = table2.common_column;
    ```
    

### RIGHT JOIN: 오른쪽 테이블을 기준으로 한 조인

- **RIGHT JOIN**: 오른쪽 테이블의 모든 행과 왼쪽 테이블에서 일치하는 행을 반환.
    
    ```sql
    SELECT table1.column1, table2.column2
    FROM table1
    RIGHT JOIN table2 ON table1.common_column = table2.common_column;
    ```

## [실습] 조인

```sql
-- 작가와 그 작가의 책 조회 (JOIN 사용)
SELECT a.name AS author_name, b.title AS book_title, b.publication_date
FROM books b
INNER JOIN authors a ON b.author_id = a.author_id;
```
