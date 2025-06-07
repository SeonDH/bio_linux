# [실습] rsync - 5분

## 실습 전 준비

```bash
mkdir ~/rsync
cd ~/rsync
```


## 실습 문제

1. 로컬 PC에서 `rsync` 디렉터리를 생성한다.
2. 로컬 PC에 `from_local1` 파일을 생성한다.
3. 다음 명령어를 이용하여 원격 서버와 디렉터리를 동기화한다.

```bash
rsync -e 'ssh -p 1119 -o Ciphers=aes256-cbc' -avz ./from_local user{]@koreabio.limeops.co.kr:/BiO/Access/home/user31/rsync
```

4. 로컬 PC에 `from_local2` 파일을 추가로 생성한다.
5. 다시 위의 `rsync` 명령어를 사용하여 디렉터리를 동기화한다.