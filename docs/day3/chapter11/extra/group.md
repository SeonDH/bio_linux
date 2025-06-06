# [번외] 사용자 그룹과 사용자 변경

## 그룹

리눅스는 사용자를 그룹으로 묶어 권한을 일괄적으로 관리할 수 있도록 한다.
한 사용자는 기본 그룹 외에도 여러 보조 그룹에 속할 수 있다.

| 구분    | 설명                |
| ----- | ----------------- |
| 기본 그룹 | 로그인 시 자동으로 속하는 그룹 |
| 보조 그룹 | 추가로 속할 수 있는 그룹    |


## 그룹 관리 명령어

### 그룹 생성

```bash
sudo groupadd groupname
```

### 그룹 삭제

그룹이 비어 있는 경우에만 삭제할 수 있다.

```bash
sudo groupdel groupname
```

### 그룹 이름 변경

```bash
sudo groupmod -n newname oldname
```



## 사용자와 그룹 관계 확인 및 설정

### 사용자 그룹 확인

```bash
groups 사용자이름
id 사용자이름
```

### 사용자에게 그룹 추가

```bash
sudo usermod -aG 그룹이름 사용자이름
```

* `-aG` 옵션은 기존 그룹을 유지하면서 새 그룹을 추가한다.

### 사용자 기본 그룹 변경

```bash
sudo usermod -g 그룹이름 사용자이름
```

## 파일 소유자 및 그룹 변경

### chown 명령어

| 명령어                              | 설명            |
| -------------------------------- | ------------- |
| `chown new_owner file`           | 소유자 변경        |
| `chown :new_group file`          | 그룹 변경         |
| `chown new_owner:new_group file` | 소유자와 그룹 동시 변경 |

```bash
chown user:group example.txt
```

### chgrp 명령어

`chgrp` 명령어는 그룹만 변경할 때 사용한다.

```bash
chgrp new_group example.txt
```