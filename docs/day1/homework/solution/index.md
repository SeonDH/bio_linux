# Day 1 과제 답지 예시

아래 예시는 로컬 Linux에 SSH로 접속한 뒤 실행한다.

## 1. 과제 디렉터리 생성

```bash
mkdir -p ~/linux_homework/day1
cd ~/linux_homework/day1
pwd
```

## 2. `vi`로 문서 만들기

```bash
vi memo.txt
```

예시 내용:

```text
Day 1 Linux homework
SSH login and file practice
```

저장:

```text
Esc
:wq
Enter
```

## 3. 심볼릭 링크 만들기

```bash
ln -s ~/linux_homework/day1/memo.txt ~/memo_link.txt
ls -l ~/memo_link.txt
cat ~/memo_link.txt
```
