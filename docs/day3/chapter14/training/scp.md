# [실습] scp

## 실습 전 준비

```bash
mkdir ~/scp
cd ~/scp
```


## 실습 문제

1. 로컬 PC에서 `from_local` 파일을 생성한 후, `scp`를 사용하여 원격 서버의 `~/scp` 디렉터리로 전송한다.
2. 리눅스 서버의 `from_linux` 파일을 로컬 PC로 복사한다.

### 참고 명령어 (로컬에서 날려야한다)

#### 로컬 → 서버

```bash
scp -P 1119 ./from_local user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp 
```

#### 서버 → 로컬

```bash
scp -P 1119 -o user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp/from_linux . Ciphers=aes256-cbc 
```