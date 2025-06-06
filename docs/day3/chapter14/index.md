---
title: "14. 서버와 파일 전송"
nav_order: 20
layout: default
---

# 14. 서버와 파일 전송


## SSH 암호 인증 없이 로그인하기

- [[번외] SSH 키 등록](extra/ssh_key.md)


## 파일 전송: `scp`

* `scp`는 SSH 프로토콜을 기반으로 파일을 전송하는 명령어이다.
* 로컬에서 원격 서버로 또는 반대로 파일을 복사할 수 있다.

### 로컬 → 원격

```bash
scp /path/to/local/file username@remote_host:/path/to/remote/
```


### 원격 → 로컬

```bash
scp username@remote_host:/path/to/remote/file /path/to/local/
```


### [실습] scp

- [실습] [scp - 5분](training/scp.md)



## 디렉터리 동기화: `rsync`

* `rsync`는 파일과 디렉터리를 동기화하는 명령어이다.
* `scp`와 달리 변경된 내용만 전송하여 효율적이다.
* SSH 기반으로 사용 가능하며, 양쪽 모두 `rsync`가 설치되어 있어야 한다.

### 로컬 → 원격

```bash
rsync -avz /path/to/local/directory/ username@remote_host:/path/to/remote/
```



### [실습] rsync

- [[실습] rsync - 5분](training/rsync.md)



## 포트를 통한 파일 전송: `nc` (netcat)

* `nc`는 TCP/UDP 포트를 통해 데이터를 전송하는 도구이다.
* 네트워크 포트가 열려 있어야 하며, 단순하고 빠른 전송이 가능하다.
* 테스트는 로컬 환경에서 가능하다.

### 받는 쪽 (서버)

```bash
nc -l -p 포트번호 | tar xzf -
```

### 보내는 쪽 (로컬)

```bash
tar czf - directory | nc remote_host 포트번호
```



### \[실습] nc

- [실습] [nc - 5분](training/nc.md)



## HTTP/HTTPS를 통한 파일 다운로드

### wget 사용

```bash
wget http://example.com/path/to/file
```

### curl 사용

```bash
curl -O http://example.com/path/to/file
```



## Git을 이용한 전송

Git은 내부적으로 SSH, HTTPS, Git 프로토콜을 모두 지원한다.

```bash
git clone ssh://username@hostname/path/to/repository.git
git clone https://hostname/path/to/repository.git
git clone git://hostname/path/to/repository.git
```

> 자세한 내용은 18장에서 다룬다.


## 파일 압축 및 해제

### 1. `tar` 명령어

* 여러 파일을 하나의 아카이브로 묶는다.
* `tar` 자체는 압축하지 않으며, gzip, bzip2와 함께 사용 가능하다.

#### 주요 옵션

| 옵션  | 설명                  |
| --- | ------------------- |
| `c` | 아카이브 생성 (create)    |
| `x` | 압축 해제 (extract)     |
| `v` | 처리 과정을 출력 (verbose) |
| `f` | 파일 이름 지정 (file)     |
| `z` | gzip 사용             |
| `j` | bzip2 사용            |

#### 예시

```bash
# 단순 압축
tar -cvf archive.tar file1 file2 dir/

# 압축 해제
tar -xvf archive.tar

# gzip 압축
tar -czvf archive.tar.gz file1 dir/

# gzip 해제
tar -xzvf archive.tar.gz

# bzip2 압축
tar -cjvf archive.tar.bz2 file1 dir/

# bzip2 해제
tar -xjvf archive.tar.bz2
```

### 2. `gzip` 명령어

```bash
# 압축
gzip filename

# 압축 해제
gzip -d filename.gz

# 압축 파일 내용 보기
zcat filename.gz
zgrep pattern filename.gz
```

### 3. `bzip2` 명령어

```bash
# 압축
bzip2 filename

# 압축 해제
bzip2 -d filename.bz2

# 압축 파일 내용 보기
bzcat filename.bz2
bzgrep pattern filename.bz2
```

### 4. `zip` 및 `unzip` 명령어

```bash
# zip 압축
zip archive.zip file1 file2 dir/

# zip 디렉터리 전체 압축
zip -r archive.zip dir/

# 압축 해제
unzip archive.zip
```



### [실습] 파일 압축

- [실습] [파일 압축 해제 - 10분](training/zip_unzip.md)