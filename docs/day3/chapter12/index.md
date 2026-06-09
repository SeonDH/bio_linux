---
title: "12. 프로세스 관리"
nav_order: 18
layout: default
---


# 12. 프로세스 관리

## 프로세스의 개념

* 프로세스는 실행 중인 프로그램을 의미한다.
* 프로그램이 메모리에 적재되어 CPU에서 실행되면 프로세스가 된다.

## 프로세스의 구성 요소

* **텍스트 섹션**: 실행할 코드가 저장된 공간
* **프로그램 카운터 (PC)**: 다음 명령어의 주소를 가리킴
* **레지스터**: CPU 내의 임시 저장 장치
* **스택**: 함수 호출, 지역 변수 저장
* **데이터 섹션**: 전역 변수 저장 공간
* **힙**: 실행 중 동적으로 할당된 메모리 영역

## 프로세스 상태

| 상태                        | 설명                        |
| ------------------------- | ------------------------- |
| R (Running)               | 실행 중이거나 실행 가능한 상태         |
| S (Sleeping)              | 이벤트(예: I/O) 대기 중          |
| D (Uninterruptible Sleep) | 중단 불가능한 대기 상태 (디스크 I/O 등) |
| T (Stopped)               | 일시 중지된 상태                 |
| Z (Zombie)                | 종료되었지만 부모가 상태를 회수하지 않음    |
| I (Idle)                  | 유휴 상태의 커널 스레드             |
| X (Dead)                  | 종료된 상태                    |

## 프로세스 정보 구조

* **PID**: 프로세스 고유 식별자
* **PPID**: 부모 프로세스의 PID
* **UID**: 사용자 ID
* **GID**: 그룹 ID

## 프로세스 상태 확인 명령어 (`ps`)

* `ps`는 실행 중인 프로세스의 정보를 출력한다.

| 명령어           | 설명                |
| ------------- | ----------------- |
| `ps -e`       | 전체 프로세스 출력        |
| `ps -f`       | 풀 포맷으로 출력         |
| `ps -u {사용자}` | 특정 사용자의 프로세스 출력   |
| `ps aux`      | 상세한 전체 프로세스 목록 출력 |

## 프로세스 종료 명령어

### kill

* `kill` 명령어는 특정 PID에 종료 신호를 보낸다.

```bash
kill [옵션] PID
```

| 시그널            | 설명             |
| -------------- | -------------- |
| `SIGTERM` (15) | 정상 종료 요청 (기본값) |
| `SIGKILL` (9)  | 강제 종료          |

### pkill

* `pkill` 명령어는 프로세스 이름을 기준으로 종료한다.

```bash
pkill [옵션] 프로세스이름
```

### pgrep

* `pgrep` 명령어는 프로세스 이름을 기준으로 PID를 찾는다.
* `ps`와 `grep`을 조합하는 것보다 간단하게 특정 프로세스의 PID를 확인할 수 있다.

```bash
pgrep [옵션] 프로세스이름
```

예:

```bash
pgrep -f sleep_script.sh
```

> `-f` 옵션은 실행 명령 전체에서 문자열을 찾는다.

## ps와 kill 조합

`ps` 명령어로 PID를 확인한 뒤 `kill` 명령어로 종료하는 방식으로 원하는 프로세스를 제어할 수 있다.


### ps와 kill을 조합해 원하는 프로세스를 종료할 수 있다.

## [실습] PS 실습

[[실습] ps 실습 - 10분](training/ps.md)


## kill 스크립트에서 활용

장시간 실행되는 스크립트는 실행할 때 PID를 파일로 남겨두면 나중에 `kill` 명령어로 종료하기 쉽다.

- 실행 스크립트가 자기 자신의 PID를 파일에 저장한다.
- 종료 스크립트는 PID 파일을 읽어 해당 프로세스를 종료한다.
- 종료 후에는 PID 파일을 삭제해 다음 실행 때 혼동을 줄인다.

간단한 흐름은 다음과 같다.

```bash
# 실행 스크립트 작성
vi start_sleep.sh

# 종료 스크립트 작성
vi stop_sleep.sh

# 실행 권한 부여
chmod +x start_sleep.sh stop_sleep.sh

# 백그라운드 실행
./start_sleep.sh &

# 저장된 PID 확인
cat sleep_script.pid

# PID 파일을 이용해 종료
./stop_sleep.sh
```

아래 예시에서 `echo $$ > "$PIDFILE"`은 현재 실행 중인 스크립트의 PID를 `sleep_script.pid` 파일에 저장한다는 뜻이다.

- `$$`: 현재 실행 중인 셸 스크립트의 PID
- `>`: 왼쪽 명령어의 출력 결과를 파일에 저장
- `"$PIDFILE"`: PID를 저장할 파일 이름, 여기서는 `sleep_script.pid`

즉 `echo $$ > "$PIDFILE"`은 현재 스크립트의 PID를 화면에 출력하지 않고 `sleep_script.pid` 파일에 기록한다.

### 실행 스크립트: `start_sleep.sh`

스크립트가 시작되면 자신의 PID를 `sleep_script.pid` 파일에 저장한다.

```bash
#!/bin/bash
PIDFILE="sleep_script.pid"
echo $$ > "$PIDFILE"

cleanup() {
  rm -f "$PIDFILE"
  exit 0
}

trap cleanup EXIT SIGTERM SIGINT

while true; do
  echo "Running... $(date)"
  sleep 1
done
```

### 종료 스크립트: `stop_sleep.sh`

PID 파일에서 프로세스 번호를 읽어 실행 중인 스크립트를 종료한다.

```bash
#!/bin/bash
PIDFILE="sleep_script.pid"

if [ -f "$PIDFILE" ]; then
  PID=$(cat "$PIDFILE")
  echo "Stopping process with PID: $PID"
  kill "$PID"
  rm -f "$PIDFILE"
else
  echo "PID file does not exist."
fi
```

### `trap`과 종료 신호

`trap`은 셸 스크립트에서 특정 신호나 종료 상황이 발생했을 때 실행할 명령을 등록하는 기능이다.

위 실행 스크립트의 핵심은 다음 부분이다.

```bash
cleanup() {
  rm -f "$PIDFILE"
  exit 0
}

trap cleanup EXIT SIGTERM SIGINT
```

`trap cleanup EXIT SIGTERM SIGINT`는 스크립트가 종료되거나 종료 요청을 받았을 때 `cleanup` 함수를 실행하라는 뜻이다. 이 예제에서는 스크립트가 끝날 때 `sleep_script.pid` 파일을 자동으로 삭제한다.

프로세스 제어에서 자주 만나는 신호는 다음과 같다.

| 신호 | 발생 상황 | 설명 |
| --- | --- | --- |
| `SIGINT` | `Ctrl + C` 입력 | 사용자가 현재 실행 중인 작업을 중단 |
| `SIGTERM` | `kill PID` 실행 | 프로세스에 정상 종료 요청 |
| `SIGHUP` | 터미널 또는 SSH 연결 종료 | 연결이 끊겼음을 알림 |
| `SIGKILL` | `kill -9 PID` 실행 | 즉시 강제 종료, `trap`으로 처리할 수 없음 |
| `EXIT` | 셸 스크립트 종료 | 스크립트가 끝날 때 정리 작업 실행 |

`trap`은 PID 파일 삭제, 임시 파일 삭제, 로그 남기기처럼 스크립트 종료 전에 정리해야 할 작업에 자주 사용된다.

### `kill`과 `kill -9` 비교

`kill PID`는 기본적으로 `SIGTERM` 신호를 보내 정상 종료를 요청한다. 이 경우 스크립트는 종료되기 전에 `trap`에 등록된 정리 작업을 실행할 수 있다.

```bash
# 스크립트 실행
./start_sleep.sh &

# PID 확인
cat sleep_script.pid

# 정상 종료 요청
kill $(cat sleep_script.pid)

# 정리 작업이 실행될 시간을 잠시 기다림
sleep 2

# PID 파일이 삭제되었는지 확인
ls sleep_script.pid 2>/dev/null || echo "PID 파일이 삭제됨"
```

반면 `kill -9 PID`는 `SIGKILL` 신호를 보내 프로세스를 즉시 강제 종료한다. 이 신호는 프로세스가 처리할 수 없으므로 `trap cleanup EXIT`도 실행되지 않는다.

```bash
# 다시 실행
./start_sleep.sh &

# 강제 종료
kill -9 $(cat sleep_script.pid)

# 강제 종료 후 상태 확인을 위해 잠시 기다림
sleep 2

# trap이 실행되지 않았기 때문에 PID 파일이 남아 있을 수 있다
ls sleep_script.pid

# 남은 PID 파일 정리
rm -f sleep_script.pid
```

따라서 먼저 `kill PID`로 정상 종료를 시도하고, 그래도 종료되지 않을 때만 `kill -9 PID`를 사용하는 것이 좋다.

## 시스템 자원의 이해: CPU, 메모리, 디스크

리눅스에서 실행 중인 작업은 CPU, 메모리, 디스크, 네트워크 같은 자원을 사용한다. 프로세스가 느리거나 멈춘 것처럼 보일 때는 어떤 자원이 부족한지 먼저 확인해야 한다.

| 자원 | 역할 | 부족할 때 나타나는 현상 | 확인 명령어 |
| --- | --- | --- | --- |
| CPU | 계산 수행 | 계산 작업이 오래 걸리고 load average가 높아짐 | `top`, `htop`, `uptime` |
| 메모리 | 실행 중인 프로그램과 데이터를 보관 | swap 사용 증가, 전체 시스템 속도 저하, 작업 종료 | `free -h`, `top` |
| 디스크 | 파일 저장 공간과 읽기/쓰기 | 파일 읽기/쓰기 지연, 용량 부족 오류 | `df -h`, `du -h`, `iostat` |
| 네트워크 | 원격 서버와 데이터 송수신 | 다운로드/업로드 지연, 접속 실패 | `ping`, `ss`, `scp`, `rsync` |

바이오 데이터 분석에서는 FASTQ, BAM, VCF처럼 큰 파일을 다루는 일이 많다. CPU가 남아 있어도 디스크 읽기/쓰기가 느리면 전체 작업이 느릴 수 있고, 메모리가 부족하면 swap을 사용하면서 작업 속도가 크게 떨어질 수 있다.

### CPU, 메모리, 디스크 I/O의 관계

리눅스에서 `디스크`는 저장 공간 자체를 뜻하고, `디스크 I/O(Input/Output)`는 그 저장 공간에서 파일을 읽고 쓰는 동작을 뜻한다.

- CPU는 계산을 수행한다.
- 메모리는 지금 실행 중인 데이터와 중간 결과를 잠시 보관한다.
- 디스크 I/O는 큰 파일을 읽고 쓰는 작업을 담당한다.

이 셋은 서로 영향을 준다.

- 메모리가 부족하면 운영체제가 디스크의 swap 공간을 사용하게 되고, 그만큼 디스크 I/O가 늘어난다.
- 디스크 I/O가 느리면 CPU가 할 일이 있어도 데이터를 기다리면서 전체 작업 속도가 떨어진다.
- 반대로 CPU 연산이 많은 작업은 디스크보다 계산 성능이 더 중요하다.

실무에서는 “CPU 사용률은 낮은데 작업이 느리다” 또는 “메모리는 충분한데 분석이 오래 걸린다” 같은 상황이 자주 생긴다. 이럴 때는 디스크 I/O 병목인지 먼저 확인해야 한다.

대표적인 확인 명령어는 다음과 같다.

```bash
# 메모리 상태 확인
free -h

# 디스크 용량 확인
df -h

# 현재 디렉터리 하위 용량 확인
du -h --max-depth=1

# 시스템 부하 확인
uptime

# 디스크 I/O 상태 확인
iostat
```

> `iostat`은 기본 설치되어 있지 않을 수 있다. Ubuntu에서는 `sudo apt install sysstat`으로 설치할 수 있다.


## ps 활용 예제

```bash
#!/bin/bash

# CPU 사용률이 80% 이상인 프로세스
echo "=== CPU 사용률이 80% 이상인 프로세스 ==="
ps aux --sort=-%cpu | awk '$3>80 {print $0}'

# 메모리 사용률이 80% 이상인 프로세스
echo "=== 메모리 사용률이 80% 이상인 프로세스 ==="
ps aux --sort=-%mem | awk '$4>80 {print $0}'

# 좀비 프로세스
echo "=== 좀비 프로세스 ==="
ps aux | awk '$8=="Z" {print $0}'

echo "=== 확인 완료 ==="
```



## top 명령어

`top`은 시스템에서 실행 중인 프로세스 상태를 **실시간으로 모니터링**할 수 있는 명령어

```bash
top
```

| 단축키        | 기능                     |
|---------------|--------------------------|
| `Shift + P`   | CPU 사용률 순 정렬       |
| `Shift + M`   | 메모리 사용률 순 정렬    |
| `Shift + T`   | 실행 시간 순 정렬        |
| `u`           | 특정 사용자 필터링       |
| `p`           | 특정 PID 필터링          |
| `q`           | 종료                     |


- 특정 사용자의 프로세스만 볼 수 있다
    
  ```bash
  top -u {username}
  ```
    
- 특정 PID 정보만 볼 수 있다

  ```bash
  top -p PID
  ```


[[번외] 서버 상태 보기](extra/server_status.md)

[[번외] 리눅스 프로세스 동작 방식](extra/process_deep.md)
