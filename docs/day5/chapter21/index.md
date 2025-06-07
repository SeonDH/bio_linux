---
title: "21. 터미널 여러개 관리하기 (screen, tmux)"
nav_order: 27
layout: default
---

# 21. 터미널 여러개 관리하기 (screen, tmux)

## screen & tmux

- 리눅스에서 터미널 멀티플렉싱을 위한 도구이다.
- 이들 도구를 사용하면 하나의 터미널 세션에서 여러 창을 열고, 세션을 백그라운드로 보내거나, 세션을 분리했다가 다시 연결할 수 있다. 이는 특히 원격 서버에서 작업할 때 유용하다.
- 특징: 내가 터미널을 닫아도 세션이 그대로 남아있는다 (exit로 명시적으로 종료하는 경우 사라짐)

## screen

### screen 관련 설정 파일 생성

```bash
$ vi ~/.screenrc
```

#### .screenrc

```
# 기본 접두사 키를 Ctrl-b로 변경
# escape ^Bb

# 상태 표시줄 설정
hardstatus alwayslastline
hardstatus string '%{= kG}[%H] %{= kw}%-Lw%{= kW}%n*%f %t%{= kw}%+Lw %= %Y-%m-%d %c'

# 새 창의 기본 쉘
shell -$SHELL

# 기본 창 이름 설정
screen -t main

# 창 번호 표시
caption always
caption string '%{= kw}Window: %n %t'
```

### 기본 명령어

1. **새 세션 시작**
    
    ```bash
    screen
    ```
    
2. **이름을 지정하여 새 세션 시작**
    
    ```bash
    screen -S session_name
    ```
    
3. **세션 분리 (detach)**
    
    ```bash
    Ctrl + a, d
    ```
    
4. **분리된 세션에 재연결**
    
    ```bash
    screen -r
    ```
    
5. **현재 세션 목록 보기**
    
    ```bash
    screen -ls
    ```
    
6. **특정 세션에 연결**
    
    ```bash
    screen -r session_name
    ```
    
7. **새 창 만들기**
    
    ```bash
    Ctrl + a, c
    ```
    
8. **창 간 전환**
    
    ```bash
    Ctrl + a, n  # 다음 창으로 이동
    Ctrl + a, p  # 이전 창으로 이동
    ```
    
9. **창 이름 지정**
    
    ```bash
    Ctrl + a, A
    ```
    
10. **세션 내 창 목록 보기**
    
    ```bash
    Ctrl + a, "
    ```
    
11. **특정 창으로 이동**
    
    ```bash
    Ctrl + a, <숫자>
    ```
    
12. **스크롤 모드로 전환**
    
    ```bash
    Ctrl + a +  [
    ```
    
13. **화면 분할 (창 분할 후 이동해서 새롭게 창을 만들어야 함)**
    
    ```bash
    Ctrl + a, S  # 수평 분할
    Ctrl + a, |  # 수직 분할 (| 대신 \\ 사용 가능)
    ```
    
14. **분할된 화면 간 이동**
    
    ```bash
    Ctrl + a, Tab
    ```
    
15. **분할된 화면 제거**
    
    ```bash
    Ctrl + a, X
    ```
    
16. **외부에서 세션 죽이기**
    
    ```bash
    screen -S session_name -X quit
    ```
    

## tmux

## tmux 설정 파일 생성

```bash
$ vi ~/.tmux.conf
```

### .tmux.conf 예제

```
# 기본 접두사 키를 Ctrl-a로 변경
#set -g prefix C-a
#unbind C-b
#bind C-a send-prefix

# 상태 표시줄 설정
set -g status-bg colour235
set -g status-fg white
set -g status-left '[#S]'
set -g status-right '[%Y-%m-%d %H:%M:%S]'

# 창 간 이동 시 표시줄 유지
setw -g monitor-activity on
set -g visual-activity on

# 마우스 지원 활성화
#set -g mouse on

# 창 동기화 단축키 설정
#bind s setw synchronize-panes on
#bind S setw synchronize-panes off

# 기존 수직 분할 바인딩 해제 및 새로운 바인딩 추가
#unbind %
#bind | split-window -h

# 기존 수평 분할 바인딩 해제 및 새로운 바인딩 추가
#unbind '"'
#bind - split-window -v
```

### 기본 명령어

1. **새 세션 시작**
    
    ```bash
    tmux
    ```
    
2. **이름을 지정하여 새 세션 시작**
    
    ```bash
    tmux new-session -s session_name
    ```
    
3. **세션 분리 (detach)**
    
    ```bash
    Ctrl + b, d
    ```
    
4. **분리된 세션에 재연결**
    
    ```bash
    tmux attach-session -t session_name
    ```
    
5. **현재 세션 목록 보기**
    
    ```bash
    tmux list-sessions
    ```
    
6. **특정 세션에 연결**
    
    ```bash
    tmux attach-session -t session_name
    ```
    
7. **새 창 만들기**
    
    ```bash
    Ctrl + b, c
    ```
    
8. **창 간 전환**
    
    ```bash
    Ctrl + b, n  # 다음 창으로 이동
    Ctrl + b, p  # 이전 창으로 이동
    ```
    
9. **창 이름 지정**
    
    ```bash
    Ctrl + b, ,
    ```
    
10. **세션 내 창 목록 보기**
    
    ```bash
    Ctrl + b, w
    ```
    
11. **특정 창으로 이동**
    
    ```bash
    Ctrl + b, <숫자>
    ```
    
12. **스크롤 모드로 전환**
    - Esc를 통해서 돌아올 수 있으며, 이동은 vi의 이동과 문법이 비슷하다.
    
    ```bash
    Ctrl + b, [
    ```
    
13. **화면 분할 (창 분할 후 이동해서 새롭게 창을 만들어야 함)**
    
    ```bash
    Ctrl + b, "  # 수평 분할
    Ctrl + b, %  # 수직 분할
    ```
    
14. **분할된 화면 간 이동**
    
    ```bash
    Ctrl + b, 화살표 키
    ```
    
15. **분할된 화면 제거**
    
    ```bash
    Ctrl + b, x
    ```
    
16. **동기화된 창 (동일한 명령어를 모든 창에 실행)**
    
    ```bash
    Ctrl + b, :setw synchronize-panes on
    ```
    
    - 비활성화하려면
    
    ```bash
    Ctrl + b, :setw synchronize-panes off
    ```
    


### 요약

- `screen`과 `tmux`는 터미널 멀티플렉서로, 하나의 터미널 세션에서 여러 창과 패널을 관리할 수 있다.
- `screen`은 간단한 작업에 적합하며, 오래된 시스템에서도 사용할 수 있다.
- `tmux`는 더 많은 기능과 사용자 정의 가능성을 제공하며, 최신 시스템에서의 사용에 적합하다.