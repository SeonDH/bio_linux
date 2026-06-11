# [번외] 마운트 명령어

> 아래 예시는 모두 학습용 샘플값이다. IP 주소, 사용자명, 공유 이름은 실제 환경에 맞게 바꿔야 한다.

마운트는 외부 저장소를 내 리눅스의 특정 디렉터리에 붙여서 사용하는 방식이다.
실제 서버/NAS 설정은 기관마다 다르므로, 수업에서는 클라이언트에서 붙여 쓰는 기본 명령 형태만 확인한다.

## 1. 현재 마운트 상태 확인

```bash
df -h
mount
lsblk
```

| 명령어 | 의미 |
| --- | --- |
| `df -h` | 마운트된 파일 시스템의 용량 확인 |
| `mount` | 현재 마운트된 항목 확인 |
| `lsblk` | 디스크 장치와 마운트 위치 확인 |

## 2. USB 또는 외부 디스크 마운트

외부 디스크 장치명이 `/dev/sdb1`이고, `/mnt/usb`에 붙인다고 가정한다.

```bash
sudo mkdir -p /mnt/usb
sudo mount /dev/sdb1 /mnt/usb
df -h
ls /mnt/usb
```

해제:

```bash
sudo umount /mnt/usb
```

## 3. NFS NAS 마운트

리눅스 서버나 NAS에서 NFS로 공유한 디렉터리를 붙이는 방식이다.

필요 패키지:

```bash
sudo apt install nfs-common
```

마운트:

```bash
sudo mkdir -p /mnt/nas
sudo mount -t nfs 192.168.0.10:/data/share /mnt/nas
df -h
ls /mnt/nas
```

해제:

```bash
sudo umount /mnt/nas
```

## 4. Samba/CIFS NAS 마운트

Windows 공유 폴더나 일부 NAS는 Samba(CIFS) 방식으로 접근한다.

필요 패키지:

```bash
sudo apt install cifs-utils
```

마운트:

```bash
sudo mkdir -p /mnt/samba
sudo mount -t cifs //192.168.0.10/share /mnt/samba -o username=USER
df -h
ls /mnt/samba
```

비밀번호는 실행 중 입력한다.
실제 운영 환경에서는 비밀번호를 명령어에 직접 적지 않는 것이 좋다.

해제:

```bash
sudo umount /mnt/samba
```

## 5. SSHFS 마운트

SSH 접속이 가능한 서버의 디렉터리를 로컬 디렉터리처럼 붙여 쓰는 방식이다.

필요 패키지:

```bash
sudo apt install sshfs
```

마운트:

```bash
mkdir -p ~/remote
sshfs user@192.168.0.20:/home/user ~/remote
ls ~/remote
```

해제:

```bash
fusermount -u ~/remote
```

## 6. 마운트할 때 주의할 점

- 마운트 경로는 비어 있는 디렉터리를 사용하는 것이 좋다.
- 마운트한 디렉터리 안에서 작업 중이면 `umount`가 실패할 수 있다.
- NAS나 외부 서버 파일은 네트워크 상태에 따라 느릴 수 있다.
- 대용량 분석 파일을 읽고 쓸 때는 저장소 용량과 권한을 먼저 확인한다.
- 자동 마운트(`/etc/fstab`)는 편하지만, 잘못 설정하면 부팅에 문제가 생길 수 있으므로 관리자와 상의한다.
