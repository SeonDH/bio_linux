# [번외] 와일드 카드와 대괄호 패턴

### 와일드카드(Wildcards)

와일드카드는 패턴 매칭을 위해 사용되며, `find` 명령어에서 자주 사용되는 와일드카드는 다음과 같다

1. `*` (애스터리스크)
    - 모든 문자를 0개 이상 매칭한다.
    - 예: `find . -name "*.txt"`는 현재 디렉토리와 그 하위 디렉토리에서 `.txt`로 끝나는 모든 파일을 찾는다.
2. `?` (물음표)
    - 임의의 한 문자를 매칭한다.
    - 예: `find . -name "file?.txt"`는 `file1.txt`, `fileA.txt` 등 한 글자가 채워진 모든 파일을 찾는다.

### 대괄호([]) 패턴

대괄호 패턴은 특정 문자 집합 중 하나를 매칭한다.

1. `[abc]`
    - `a`, `b`, `c` 중 하나의 문자를 매칭한다.
    - 예: `find . -name "file[123].txt"`는 `file1.txt`, `file2.txt`, `file3.txt`를 찾는다.
2. `[a-z]`
    - 소문자 알파벳 중 하나를 매칭한다.
    - 예: `find . -name "file[a-z].txt"`는 `filea.txt`, `fileb.txt`, ..., `filez.txt`를 찾는다.
3. `[0-9]`
    - 숫자 중 하나를 매칭한다.
    - 예: `find . -name "file[0-9].txt"`는 `file0.txt`, `file1.txt`, ..., `file9.txt`를 찾는다.

### 조합 예시

1. `find . -name "file[1-3]?.txt"`
    - `file1A.txt`, `file2B.txt`, `file3C.txt` 등 `file1`, `file2`, `file3`로 시작하고 그 뒤에 한 문자가 추가된 모든 `.txt` 파일을 찾는다.
2. `find . -name "[A-Z]*.log"`
    - 대문자로 시작하고 `.log`로 끝나는 모든 파일을 찾는다. 예를 들어, `App.log`, `Server.log` 등이 포함된다.