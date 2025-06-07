# [실습] 파일 압축 해제 - 10분

## 실습 전 준비

```bash
mkdir -p ~/zip/inner
cd ~/zip
touch file1 file2 file3 inner/inner_file1 inner/inner_file2
mkdir -p ~/zip2
```

## 실습 문제

1. `tar` 명령어를 이용하여 `~/zip` 하위 파일과 디렉터리를 압축한다.
2. 압축 파일을 `~/zip2/tar` 디렉터리에 해제한다.
3. `tar`와 `gzip`을 함께 사용하여 `~/zip` 하위 파일들을 압축한다.
4. 압축 파일을 `~/zip2/gzip` 디렉터리에 해제한다.
5. `tar`와 `bzip2`를 함께 사용하여 `~/zip` 하위 파일들을 압축한다.
6. 압축 파일을 `~/zip2/bzip2` 디렉터리에 해제한다.
7. `zip` 명령어를 사용하여 `~/zip` 하위 파일들을 압축한다.
8. 압축 파일을 `~/zip2/zip` 디렉터리에 해제한다.