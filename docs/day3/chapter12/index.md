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

## ps와 kill 조합

`ps` 명령어로 PID를 확인한 뒤 `kill` 명령어로 종료하는 방식으로 원하는 프로세스를 제어할 수 있다.


### ps 와 kill 을 조합해서 원하는 프로세스를 명령어로 종료 시킬 수 있다.

## [실습] PS 실습

[[실습] ps 실습 - 10분](training/ps.md)


## kill 스크립트에서 활용

- 스크립트 실행 시 pid 를 반환 하는 파일을 생성


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



## 프로세스 제어 스크립트 예시

### 스크립트 실행 시 PID 저장

```bash
#!/bin/bash
PIDFILE="sleep_script.pid"
echo $$ > "$PIDFILE"

cleanup() {
  rm -f "$PIDFILE"
  exit 0
}

trap cleanup EXIT

echo "Sleeping for 100 seconds..."
sleep 100
echo "Finished."
```

### PID 기반 종료 스크립트

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