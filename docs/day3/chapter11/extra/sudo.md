# [번외] sudo 권한 제어

### /etc/sudoers 파일 수정

```bash
# 사용자 alice에게 모든 권한 부여
alice ALL=(ALL:ALL) ALL

# developers 그룹은 특정 명령만 실행 가능
%developers ALL=(ALL) /usr/bin/apt-get, /usr/bin/systemctl

# 모든 사용자에게 비밀번호 없이 일부 명령 허용
ALL ALL=(ALL) NOPASSWD: /usr/bin/apt-get, /usr/bin/apt, /bin/cat
```

### 사용자에게 sudo 권한 부여

```bash
sudo usermod -aG sudo 사용자이름
```

* 전체 sudo 권한을 부여한다.

### 특정 명령어만 허용

```bash
john ALL=(ALL) /usr/bin/apt-get
```

| 방법              | 특징                         |
| --------------- | -------------------------- |
| sudo 그룹 추가      | 모든 sudo 명령 가능. 간단하지만 제한 없음 |
| /etc/sudoers 수정 | 특정 명령만 허용하는 세밀한 제어 가능      |