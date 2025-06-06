# 9. 파일 내용 다루기

# 파일 내용 확인

- 환경 구성

```bash
$ cd ~
$ mkdir file
$ cd file
$ seq 1 200 | sed 's/^/line /' > practice.txt
```

### 1. `cat` 명령어

- 파일의 전체 내용을 출력한다.

```bash
cat practice.txt
```

### 2. `less` 명령어

- 파일의 내용을 페이지 단위로 출력하며, 스크롤하여 내용을 볼 수 있다. `less`는 대용량 파일을 확인할 때 유용하다.

```bash
less practice.txt
```

- **주요 키**:
  - `Space`: 다음 페이지
  - `b`: 이전 페이지
  - `q`: 종료

### 3. `more` 명령어

- 파일의 내용을 페이지 단위로 출력하며, 한 번에 한 페이지씩 내용을 볼 수 있다. `more`는 `less`보다 간단한 기능을 제공한다.

```bash
more practice.txt
```

- **주요 키**:
  - `Space`: 다음 페이지
  - `Enter`: 다음 줄
  - `q`: 종료

### 4. `head` 명령어

- 파일의 처음 몇 줄을 출력한다. 기본적으로 처음 10줄을 출력하지만, 옵션을 사용하여 줄 수를 지정할 수 있다.

```bash
head practice.txt
head -n 5 practice.txt
```

### 5. `tail` 명령어

- 파일의 마지막 몇 줄을 출력한다. 기본적으로 마지막 10줄을 출력하지만, 옵션을 사용하여 줄 수를 지정할 수 있다.

```bash
tail practice.txt
tail -n 5 practice.txt
```

### 실시간 로그 모니터링

- `tail -f filename`: 파일의 마지막 부분을 실시간으로 모니터링하며, 새로운 내용이 추가되면 자동으로 출력한다.

```bash
while true; do echo "Log entry $(date)" >> logfile.txt; sleep 1; done & echo $! > mypid.txt
tail -f logfile.txt
kill $(cat mypid.txt)
```

### 6. `nl` 명령어

- 파일의 각 줄에 번호를 붙여서 출력한다.

```bash
nl practice.txt
```

### 7. `wc` 명령어

- 파일의 단어, 줄, 바이트, 문자 수를 계산한다.
- `wc -l`: 라인 수
- `wc -w`: 단어 수

```bash
wc practice.txt
```

# 파일 검색

### 1. `find` 명령어

- 파일 시스템에서 파일이나 디렉터리를 검색하는 데 사용된다.

- 환경 구성
  ```bash
  cd ~
  mkdir find
  cd find
  touch file1.txt file2.txt file3.log
  fallocate -l 2M 2M_FILE
  ```

- 명령어
  1. 특정 디렉터리에서 파일 검색:
      
      ```bash
      find . -name "file1.txt"
      ```
      
      - `.`: 검색할 디렉터리 경로
      - `name "file1.txt"`: 이름이 "filename"인 파일 검색
  2. 파일 유형별 검색:
      
      ```bash
      find . -type f -name "*.txt"
      ```
      
      - `type f`: 일반 파일 검색
      - `name "*.txt"`: 확장자가 .txt인 파일 검색
  3. 특정 시간 이내에 수정된 파일 검색:
      
      ```bash
      find . -mmin -1
      ```
      - `mmin -1`: 1분 이내에 수정된 파일 검색
      - `-mmin +1` 1분 이상 전에 수정된 파일 검색
  4. 특정 크기 이상의 파일 검색:
      
      ```bash
      find . -size +1M
      ```
      - `size -10M` : 크기가 10MB 미만인 파일 검색
      - `size 10k` : 10KB 인 파일 검색
      - `size +1M`: 크기가 1MB 초과인 파일 검색


[[번외] 와일드 카드와 대괄호 패턴](extra/wildcard.md)

## [실습] 파일 찾기

[[실습] 파일 찾기 - 10분](training/file.md)

# 리눅스 파이프라인과 필터

## 파이프라인

```bash
ls -l | more
```

## 필터

- 환경 구성
  ```bash
  cd ~
  mkdir filter
  cd filter
  cat <<EOL > example.txt
  apple,fruit,1.00
  banana,fruit,0.50
  carrot,vegetable,0.30
  banana,fruit,0.50
  apple,fruit,1.00
  eggplant,vegetable,1.20
  fig,fruit,2.00
  grape,fruit,1.80
  banana,fruit,0.50
  apple,fruit,1.00
  carrot,vegetable,0.30
  EOL
  ```


### 주요 필터 명령어

1. `grep`: 특정 패턴을 검색하고 해당 패턴이 포함된 줄을 출력한다.
    
    ```bash
    $ grep "banana" example.txt
    ```
    
2. `sed`: 스트림 에디터로, 텍스트의 변환 및 편집을 수행한다.
    
    ```bash
    $ sed 's/fruit/FRUIT/g' example.txt
    ```
    
    - 이 명령어는 `filename` 파일에서 `old`를 `new`로 바꾸는 작업을 수행한다.
3. `awk`: 데이터를 필드 단위로 처리하여 패턴 매칭 및 텍스트 변환을 수행한다.
    
    ```bash
    $ awk -F, '$2 == "fruit" { print $1 $3 }' example.txt
    ```
    
    - 이 명령어는 `filename` 파일에서 첫 번째와 세 번째 필드를 출력한다.
4. `sort`: 텍스트를 정렬한다.
    
    ```bash
    $ sort example.txt
    ```
    
5. `uniq`: 중복된 줄을 제거한다. 일반적으로 `sort`와 함께 사용된다. (파이프 라인 활용)
    
    ```bash
    $ sort example.txt | uniq
    ```
    
6. `cut`: 특정 필드를 추출한다.
    
    ```bash
    $ cut -d, -f1 example.txt
    ```
    
    - 이 명령어는 `filename` 파일에서 콤마로 구분된 첫 번째 필드를 추출한다.
7. `tr`: 문자를 변환하거나 삭제한다.
    
    ```bash
    $ tr '[:lower:]' '[:upper:]' < example.txt
    ```
    
    - 이 명령어는 `filename` 파일의 모든 소문자를 대문자로 변환한다.

## [실습] 필터 명령어 실습

[[실습] 필터 - 10분](training/filter.md)

## 파이프 라인과 필터의 조합

**파이프라인(pipe)**: 
  - `|` 기호를 사용하여 여러 명령어를 연결하고, 앞 명령의 출력을 다음 명령의 입력으로 전달하는 기능. 
  - 복잡한 작업을 간결하게 연결해 처리할 수 있다.

### 파이프라인과 필터  사용 예시 1
    - 폴더에서 `txt` 파일을 찾는 명령어
        
        ```bash
        $ ls -l | grep ".txt"
        ```
        
    - `ls -l`: 현재 디렉토리의 파일 목록을 자세히(long listing format) 출력한다.
    - `|`: 파이프라인 기호로, `ls -l` 명령어의 출력을 다음 명령어인 `grep`의 입력으로 전달한다.
    - `grep ".txt"`: 입력된 데이터에서 `.txt` 문자열이 포함된 줄만 출력한다.
### 파이프라인과 필터  사용 예시 2
    - 유니크한 데이터의 갯수를 뽑는 명령어
        
        ```bash
        $ cat example.txt | tr '[:lower:]' '[:upper:]' | sort | uniq | wc -l
        ```
        
    - `cat file.txt`: `file.txt` 파일의 내용을 출력한다.
    - `tr '[:lower:]' '[:upper:]'`: 입력된 텍스트에서 소문자를 대문자로 변환한다.
    - `sort`: 입력된 텍스트를 정렬한다.
    - `uniq`: 정렬된 텍스트에서 중복된 줄을 제거한다.
    - `wc -l` : 라인의 수를 센다
### 파이프라인과 필터 사용 예시 3
    - 디스크 사용량 찾기 (`df` 명령어는 디스크 사용량이 나오는 명령어로 나중에 배운다)
        
        ```bash
        $ df -h | grep "/dev/sda1"
        ```
        
    - `df -h`: 디스크 사용량을 사람이 읽기 쉬운 형식(human-readable)으로 출력한다.
    - `grep "/dev/sda1"`: 특정 디스크 파티션 `/dev/sda1`의 사용량 정보를 필터링하여 출력한다.

## [실습] 파이프라인과 필터 실습 - 10분

- [[실습] 파이프라인과 필터](training/pipe.md)

# 리다이렉션


- 환경 구성
  ```bash
  cd ~
  mkdir redirection
  cd redirection
  echo -e "banana\napple\ncarrot\nbanana\napple" > unsorted.txt
  touch existing_file.txt
  ```

### 리다이렉션 종류


1. **출력 리다이렉션**: 명령어의 출력을 파일로 전송한다.
    - **기본 출력 리다이렉션 (`>`)**:
        
        ```bash
        $ ls > output.txt
        ```
        
        - `ls` 명령어의 출력을 `output.txt` 파일로 저장한다. 파일이 이미 존재하면 내용을 덮어쓴다.
    - **추가 출력 리다이렉션 (`>>`)**:
        
        ```bash
        $ echo "Hello, World!" >> output.txt
        ```
        
        - `echo` 명령어의 출력을 `output.txt` 파일의 끝에 추가한다. 파일이 존재하지 않으면 새로 생성한다.
2. **입력 리다이렉션 (`<`)**: 파일의 내용을 명령어의 입력으로 사용한다.
    
    [[번외] 표준 입력과 인자의 차이](extra/diff.md)

    ```bash
    $ sort < unsorted.txt
    ```
    
    - `unsorted.txt` 파일의 내용을 `sort` 명령어의 입력으로 사용하여 정렬한다.
3. **오류 출력 리다이렉션**: 명령어의 오류 출력을 파일로 전송한다.
    - **기본 오류 출력 리다이렉션 (`2>`)**:
        
        ```bash
        $ ls non_existing_file 2> error.log
        ```
        
        - 존재하지 않는 파일을 나열하려고 할 때 발생하는 오류 메시지를 `error.log` 파일로 저장한다.
    - **오류 출력 추가 리다이렉션 (`2>>`)**:
        
        ```bash
        $ ls non_existing_file 2>> error.log
        ```
        
        - 오류 메시지를 `error.log` 파일의 끝에 추가한다.
4. **출력과 오류를 동시에 리다이렉션**:
    - **출력과 오류를 같은 파일로 리다이렉션 (`>&`)**:
        
        ```bash
        $ ls existing_file.txt non_existing_file > output.log 2>&1
        ```
        
        - 명령어의 표준 출력과 오류 출력을 모두 `output.log` 파일로 저장한다.
    - **출력과 오류를 각각 다른 파일로 리다이렉션**:
        
        ```bash
        $ ls existing_file.txt non_existing_file > output.log 2> error.log
        ```
        
        - 명령어의 표준 출력은 `output.log` 파일로, 오류 출력은 `error.log` 파일로 저장한다.

[[번외] 표준 출력과 표준 오류](extra/std.md)



## [실습] 리다이렉션

[[실습] 리다이렉션 - 10분](training/redirection.md)

## 고급 사용

[[번외] grep, sed, awk 의 고급 사용](extra/advanced.md)

# 요약

1. 리눅스는 파일의 내용을 다루기 위한 많은 명령어를 제공한다.
2. `cat`, `less`, `head`, `tail`, `wc`, `grep`, `awk` 등의 명령어는 필수적으로 익혀야 한다.
3. 파이프라인(`|`)과 리다이렉션(`>`, `>>`, `<`, `2>`)을 통해 복잡한 데이터 흐름을 유연하게 처리할 수 있다.
4. 실시간 로그 모니터링, 조건 검색, 대량 텍스트 편집 등 실무에도 자주 활용된다.