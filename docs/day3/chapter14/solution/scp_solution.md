# [답지] scp


## 명령어

아래 명령은 원격 서버에 접속한 상태가 아니라, 내 개인 PC 터미널에서 실행한다.
`user31`은 예시 계정이므로 본인에게 배정된 계정과 경로로 바꿔서 사용한다.

#### 개인 PC → 리눅스 서버

```bash
scp -o Ciphers=aes256-cbc -P 1119 ./from_local user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp/
```
#### 리눅스 서버 → 개인 PC

```bash
scp -o Ciphers=aes256-cbc -P 1119 user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp/from_linux .
```
