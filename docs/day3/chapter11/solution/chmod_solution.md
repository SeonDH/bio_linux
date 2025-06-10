# [답지] 파일 권한 변경

- 답자의 예시일 뿐이며 여러 답안도 가능하다.

1. ls -l hello.sh -> 기본 파일 권한 확인

2. ./hello.sh -> 권한 부족으로 "Permission denied"

3. chmod u+x hello.sh -> 소유자에게 실행 권한 추가

4. ./hello.sh -> "Hello, World!"