# [번외] SSH 키 등록

SSH 암호 인증 없이 로그인하려면 **SSH 키 기반 인증**을 설정해야 한다.
이 방식은 공개키 암호화 기술을 기반으로 하며, 클라이언트는 개인 키를 사용하고 서버는 공개 키로 사용자를 인증한다.

## 1. SSH 키 생성 (클라이언트 측)

로컬 컴퓨터에서 SSH 키를 생성한다.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

| 옵션        | 설명                |
| --------- | ----------------- |
| `-t rsa`  | RSA 키 유형 사용       |
| `-b 4096` | 키 길이를 4096비트로 설정  |
| `-C`      | 키에 주석 추가 (예: 이메일) |

* 명령어 실행 후 키 저장 위치와 패스프레이즈를 입력하라는 프롬프트가 나타난다.
* 기본 위치(`~/.ssh/id_rsa`, `~/.ssh/id_rsa.pub`)를 사용하거나 변경할 수 있다.
* 패스프레이즈는 생략해도 무방하다.



## 2. SSH 공개 키 복사

생성된 공개 키(`~/.ssh/id_rsa.pub`)를 원격 서버의 사용자 홈 디렉터리에 있는 `~/.ssh/authorized_keys` 파일에 추가한다.

자동으로 복사하는 명령어:

```bash
ssh-copy-id username@server_ip_address
```

또는 수동으로 복사:

```bash
cat ~/.ssh/id_rsa.pub | ssh username@server_ip_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```



## 3. SSH 설정 확인 (서버 측)

서버에서 SSH 키 인증이 허용되도록 설정 파일을 수정한다.

```bash
sudo vi /etc/ssh/sshd_config
```

다음 항목이 포함되어 있는지 확인하고, 필요 시 수정한다:

```text
PubkeyAuthentication yes
PasswordAuthentication no
ChallengeResponseAuthentication no
```

변경 후 SSH 데몬을 재시작한다.

```bash
sudo systemctl restart sshd
```



## 4. SSH 접속 테스트

이제 로컬에서 다음 명령어로 서버에 접속할 수 있다.

```bash
ssh username@server_ip_address
```

암호 없이 접속된다면 키 기반 인증 설정이 완료된 것이다.



> [[번외] 공개키 인증 방식](public_key.md)