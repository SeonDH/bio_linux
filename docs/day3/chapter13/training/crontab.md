# [실습] crontab - 10분

### 실습 전 준비

```bash
mkdir -p ~/cron
cd ~/cron
```

#### 파일 생성: `do_nothing.sh`

```bash
#!/bin/bash
# 이 스크립트는 아무 작업도 수행하지 않는다.
```

#### 파일 생성: `file_creater.sh`

※ `TARGET_DIR`에는 본인의 작업 디렉터리(절대 경로)를 입력할 것

```bash
#!/bin/bash

# 파일을 생성할 디렉터리 (절대 경로로 수정할 것)
TARGET_DIR="/home/{사용자이름}/cron"

# 현재 날짜와 시간을 기반으로 파일 이름 설정
DATE=$(date +"%Y%m%d_%H%M%S")
FILENAME="dummy_${DATE}"
FILEPATH="$TARGET_DIR/$FILENAME"

# 빈 파일 생성
touch "$FILEPATH"
```

```bash
chmod +x do_nothing.sh
chmod +x file_creater.sh 
```

### crontab 을 vi 로 열고 싶을 때 (nano 설정 시)

```
export VISUAL=vi
```

### crontab 을 nano 로 열고 싶을 떄 (vi 설정 시)

```
export VISUAL=nano
```

## 실습 문제

1. `do_nothing.sh` 스크립트를 매일 새벽 3시에 실행되도록 크론탭에 등록한다.
2. `file_creater.sh` 스크립트를 매분 실행되도록 등록한다.
3. 현재 설정된 크론탭 목록을 확인한다.
4. 등록된 크롭탭을 제거한다.

## [답지] 답지 예시

- [답지 예시](../solution/crontab_solution.md)