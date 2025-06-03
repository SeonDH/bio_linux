# \[실습] rsync - 5분

### 실습 전 명령어

```bash
mkdir ~/rsync
cd ~/rsync
```

---

### 실습 문제

1. 로컬 PC에서 `rsync` 디렉터리를 생성한다.
2. 로컬 PC에 `from_local1` 파일을 생성한다.
3. 다음 명령어를 이용하여 원격 서버와 디렉터리를 동기화한다.

```bash
rsync -e 'ssh -p 3030 -o Ciphers=aes256-cbc,aes192-cbc,aes128-cbc,3des-cbc' -avz . user31@210.216.165.57:/BiO/Access/home/user31/rsync
```

4. 로컬 PC에 `from_local2` 파일을 추가로 생성한다.
5. 다시 위의 `rsync` 명령어를 사용하여 디렉터리를 동기화한다.

---

> 이 실습은 `rsync` 명령어를 통해 **변경된 파일만 전송**되는 것을 확인하는 데 목적이 있다.
> 두 번의 동기화를 비교하면서 `rsync`의 효율성을 체감해보자.