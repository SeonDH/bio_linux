### 실습 문제

1. 로컬 PC에서 `from_local` 파일을 생성한 후, `scp`를 사용하여 원격 서버의 `~/scp` 디렉터리로 전송한다.
2. 리눅스 서버의 `from_linux` 파일을 로컬 PC로 복사한다.

---

### 참고 명령어

#### 로컬 → 서버

```bash
scp -P 3030 -o Ciphers=aes256-cbc,aes192-cbc,aes128-cbc,3des-cbc ./from_local user31@210.216.165.57:/BiO/Access/home/user31/scp
```

#### 서버 → 로컬

```bash
scp -P 3030 -o Ciphers=aes256-cbc,aes192-cbc,aes128-cbc,3des-cbc user31@210.216.165.57:/BiO/Access/home/user31/scp/from_linux .
```

---

> 이 실습은 `scp` 명령어를 통해 로컬과 서버 간 **단순 파일 복사**를 수행하는 방법을 익히는 데 목적이 있다.
> IP 주소와 포트, 암호화 옵션 등은 실제 환경에 맞게 수정해야 한다.