# [번외] 시스템 크론

## 시스템 크론이란

시스템 크론은 전체 시스템 단위의 정기 작업을 자동으로 수행하기 위한 크론 설정 방식이다.
사용자별 `crontab`과는 달리, 시스템 전체에 적용되며 보통 `root` 권한으로 설정한다.



## 시스템 크론탭 파일

### `/etc/crontab` 구조

`/etc/crontab` 파일은 시스템 전반의 크론 작업을 정의하는 대표 파일이다.
사용자 크론탭과 달리, 명령어 실행 대상 사용자를 명시해야 한다.

```cron
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# 분 시 일 월 요일 사용자 명령어
0 * * * * root /usr/bin/apt-get update
30 2 * * * root /usr/local/bin/backup.sh
```

| 필드       | 설명                  |
| -------- | ------------------- |
| 분 (0–59) | 실행 시각 (분)           |
| 시 (0–23) | 실행 시각 (시)           |
| 일 (1–31) | 실행 일자               |
| 월 (1–12) | 실행 월                |
| 요일 (0–7) | 실행 요일 (0 또는 7은 일요일) |
| 사용자      | 명령어를 실행할 사용자        |
| 명령어      | 실행할 명령어 또는 스크립트 경로  |



## `/etc/cron.d` 디렉토리

* `/etc/cron.d/` 안에 별도의 파일을 만들어 시스템 크론 작업을 분리해서 관리할 수 있다.
* 각 파일은 `/etc/crontab`과 동일한 형식을 사용한다.

```cron
# /etc/cron.d/example
0 5 * * * root /usr/local/bin/daily-maintenance
```



## 주기별 작업 디렉토리

리눅스 시스템에서는 다음과 같은 디렉토리를 통해 별도의 설정 없이 주기적인 작업을 수행할 수 있다.

| 디렉토리                 | 실행 주기 |
| -------------------- | ----- |
| `/etc/cron.hourly/`  | 매 시간  |
| `/etc/cron.daily/`   | 매일    |
| `/etc/cron.weekly/`  | 매주    |
| `/etc/cron.monthly/` | 매월    |

### 스크립트 등록 예시

```bash
# 매일 실행할 스크립트를 등록
sudo cp myscript.sh /etc/cron.daily/
```

> 해당 스크립트는 실행 권한이 있어야 하며, 셸에서 직접 실행 가능한 구조여야 한다.



## 시스템 크론 로그 확인

시스템 크론 작업의 실행 결과는 다음 경로의 로그 파일에서 확인할 수 있다.

```bash
# Debian/Ubuntu
grep CRON /var/log/syslog

# RHEL/CentOS
grep CRON /var/log/cron
```



## 시스템 크론 예시

### 예시 1: 매일 자정에 시스템 업데이트 수행

```cron
0 0 * * * root /usr/bin/apt-get update && /usr/bin/apt-get upgrade -y
```

### 예시 2: 매주 일요일 오전 2시에 백업 수행

```cron
0 2 * * 0 root /usr/local/bin/backup.sh
```



## 요약

* 시스템 크론은 루트 또는 시스템 전체 차원에서 작업을 자동화하는 방식이다.
* `/etc/crontab`, `/etc/cron.d/`, `/etc/cron.*` 디렉터리를 통해 설정할 수 있다.
* 사용자 크론탭과 다르게 사용자 필드가 포함된다.
* 실행 로그는 `/var/log/syslog` 또는 `/var/log/cron`에서 확인 가능하다.