# [번외] PowerShell에서 `vi` 사용 시 단축키 충돌 문제

Windows 환경에서 PowerShell을 사용해 `vi` 또는 `vim` 에디터를 실행할 경우, **`Ctrl + V`** 단축키가 윈도우 기본 붙여넣기 동작과 충돌하여 vim의 **비주얼 블록 모드(Visual Block Mode)** 가 정상적으로 작동하지 않을 수 있다.


## 증상

* PowerShell 또는 CMD에서 `vi` 실행 후,
  `Ctrl + V`를 눌러 비주얼 블록 모드를 시작하려고 하면 붙여넣기가 실행됨.


## 해결 방법

* `Ctrl + V` 대신 `Ctrl + Q`를 사용하면 Vim의 **비주얼 블록 모드**로 진입 가능하다.
* 이는 Vim 내부의 터미널 제어 동작과 관련되어 있으며, 일부 터미널에서 `Ctrl + Q`로 대체된다.


## 참고 링크

* StackOverflow: [vim ctrl-v conflict with windows paste](https://stackoverflow.com/questions/426896/vim-ctrl-v-conflict-with-windows-paste)


## 요약

| 동작                | 키보드 입력     | 비고                   |
| ----------------- | ---------- | -------------------- |
| 붙여넣기 (PowerShell) | `Ctrl + V` | Windows 기본 동작        |
| 블록 선택 (Vim)       | `Ctrl + Q` | `Ctrl + V` 대신 사용 가능함 |


## 참고

* Windows Terminal 또는 WSL 환경에서는 단축키 충돌이 다르게 발생할 수 있으므로, 사용하는 터미널 설정을 확인하는 것이 좋다.
* `:help visual-block` 명령어로 Vim 내부에서 관련 도움말을 확인할 수 있다.