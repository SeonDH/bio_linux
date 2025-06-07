# [번외] 마운트 명령어

# 클라이언트 설정

## 1. NFS 마운트 (리눅스 ↔ 리눅스)

- 서버에서 공유한 디렉토리를 NFS 프로토콜로 마운트


### 1-1. NFS 클라이언트 설치

```bash
sudo apt install nfs-common
```

### 1-2. 마운트 지점 생성

```bash
sudo mkdir -p /mnt/nfs
```

### 1-3. 마운트 실행

```bash
sudo mount -t cifs //192.168.0.101/share /mnt/samba -o credentials=/etc/samba/cred,iocharset=utf8

```

### 1-4. 마운트 확인

```bash
df -h
```


## 2. Samba(CIFS) 마운트 (리눅스 ↔ 윈도우)

### 2-1. CIFS 유틸 설치

```bash
sudo apt install cifs-utils
```

### 2-2. 마운트 디렉토리 생성

```bash
sudo mkdir -p /mnt/samba
```

### 2-3. 마운트 (사용자 인증 포함)

```bash
sudo mount -t cifs //192.168.0.101/share /mnt/samba -o username=USER,password=PASS
```

### 2-4. 마운트 확인

```bash
df -h
```


## 3. SSHFS 마운트 (리눅스 ↔ 리눅스)

### 3-1. SSHFS 설치

```bash
sudo apt install sshfs
```

### 3-2. 마운트 디렉토리 생성

```bash
mkdir ~/remote
```

### 3-3. 마운트 실행

```bash
sshfs user@192.168.0.102:/home/user ~/remote
```

### 3-4. 마운트 해제

```bash
fusermount -u ~/remote
```


## 마운트 해제 공통 명령어

```bash
sudo umount /mnt/nfs
sudo umount /mnt/samba
```


## 참고: 자동 마운트

* `/etc/fstab` 파일에 항목을 추가하여 부팅 시 자동 마운트 설정 가능


# 서버 설정


## 1. NFS 서버에서 디렉토리 공유 (리눅스)

### 1-1. NFS 서버 패키지 설치

```bash
sudo apt update
sudo apt install nfs-kernel-server
```

### 1-2. 공유할 디렉토리 생성
```bash
sudo mkdir -p /srv/shared
# /srv/shared 디렉토리를 클라이언트에 공유할 디렉토리로 사용
sudo chown nobody:nogroup /srv/shared
```

### 1-3. /etc/exports 파일 설정

```bash
sudo vi /etc/exports
```

아래 줄을 마지막에 추가 (192.168.0.0/24은 접근을 허용할 클라이언트 IP 대역)
```
/srv/shared 192.168.0.0/24(rw,sync,no_subtree_check)
```

### 1-4. NFS 서비스 적용 및 재시작

```bash
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

### 1-5. 방화벽 허용 (필요한 경우)

```bash
sudo ufw allow from 192.168.0.0/24 to any port nfs
```

## 2. Samba(CIFS) 서버에서 디렉토리 공유 (리눅스 → 윈도우 클라이언트용)

### 2-1. Samba 설치

```bash
sudo apt update
sudo apt install samba
```
### 2-2. 공유할 디렉토리 생성

```bash
sudo mkdir -p /srv/samba/share
sudo chown nobody:nogroup /srv/samba/share
sudo chmod 0775 /srv/samba/share
```
### 2-3. Samba 설정 파일 편집

```bash
sudo vi /etc/samba/smb.conf
```
파일 맨 아래에 다음 블록 추가:

```
[Shared]
   path = /srv/samba/share
   browsable = yes
   read only = no
   guest ok = yes
```

- guest ok = yes는 인증 없이 접근 허용. 인증 필요 시 guest ok = no로 변경하고 사용자 등록 필요.

### 2-4. Samba 서비스 재시작

```bash
sudo systemctl restart smbd
```

### 2-5. Samba 사용자 추가 (옵션)

```bash
sudo smbpasswd -a 사용자명
```
- 윈도우에서 접속 시 인증 계정으로 사용됨.

### 2-6. 방화벽 허용 (필요한 경우)

```bash
sudo ufw allow 'Samba'
```

## 3. SSHFS(SSH Filesystem)

- SSHFS는 SSH(Secure Shell) 프로토콜을 기반으로 작동하며, 클라이언트에서 SSH를 통해 원격 파일 시스템에 접근하는 방식
- 서버 측에 SSH만 열려 있으면 클라이언트가 SSHFS로 마운트 가능

