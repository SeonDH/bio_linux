# [답지] scp


## 명령어 (원격 접속을 하지 않고 내 개인 PC 에서 날려야한다)

#### 개인 PC → 리눅스 서버

```bash
scp -o Ciphers=aes256-cbc -P 1119 ./from_local user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp 
```
#### 리눅스 서버 → 개인 PC

```bash
scp -o Ciphers=aes256-cbc -P 1119 user31@koreabio.limeops.co.kr:/BiO/Access/home/user31/scp/from_linux . 
```