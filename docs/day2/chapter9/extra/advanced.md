# [번외] grep, sed, awk 의 고급 사용

`grep`, `sed`, `awk`의 고급 사용법을 익히면 리눅스에서 복잡한 텍스트 처리와 데이터 조작 작업을 매우 효율적으로 수행할 수 있다. 각 명령어의 고급 사용법을 예시와 함께 설명한다.

### `grep`의 고급 사용법

1. **여러 패턴 검색 (`e` 옵션)**
    
    ```bash
    grep -e 'pattern1' -e 'pattern2' file.txt
    ```
    
    - `file.txt`에서 `pattern1` 또는 `pattern2`를 포함하는 줄을 검색한다.
2. **정규 표현식 파일을 사용한 검색 (`f` 옵션)**
    
    ```bash
    grep -f patterns.txt file.txt
    ```
    
    - `patterns.txt` 파일에 있는 여러 패턴을 사용하여 `file.txt`에서 검색한다.
3. **일치하지 않는 줄 출력 (`v` 옵션)**
    
    ```bash
    grep -v 'pattern' file.txt
    ```
    
    - `pattern`과 일치하지 않는 줄을 출력한다.
4. **주변 줄 함께 출력 (`C`, `B`, `A` 옵션)**
    - **`C`**: 지정한 줄 수만큼 앞뒤로 함께 출력.
        
        ```bash
        grep -C 2 'pattern' file.txt
        ```
        
    - **`B`**: 지정한 줄 수만큼 앞줄과 함께 출력.
        
        ```bash
        grep -B 2 'pattern' file.txt
        ```
        
    - **`A`**: 지정한 줄 수만큼 뒷줄과 함께 출력.
        
        ```bash
        grep -A 2 'pattern' file.txt
        ```
        

### `sed`의 고급 사용법

1. **파일에서 특정 패턴을 찾아 바꾸기 (`s` 명령어)**
    - **기본 치환**
        
        ```bash
        sed 's/pattern/replacement/' file.txt
        ```
        
    - **모든 일치 항목 치환 (`g` 플래그)**
        
        ```bash
        sed 's/pattern/replacement/g' file.txt
        ```
        
2. **여러 줄을 대상으로 작업**
    - **줄 범위를 지정하여 작업**
        
        ```bash
        sed '1,3s/pattern/replacement/' file.txt
        ```
        
        - 1번 줄부터 3번 줄까지 `pattern`을 `replacement`로 바꾼다.
3. **파일 끝에 텍스트 추가 (`$a`)**
    
    ```bash
    sed '$a\\New text to append' file.txt
    ```
    
4. **줄 삽입 (`i` 명령어)**
    
    ```bash
    sed '2i\\Inserted text' file.txt
    ```
    
5. **패턴 매칭 줄 삭제 (`d` 명령어)**
    
    ```bash
    sed '/pattern/d' file.txt
    ```
    

### `awk`의 고급 사용법

1. **복잡한 조건문 사용**
    
    ```bash
    awk '$3 > 50 {print $1, $2}' file.txt
    ```
    
    - 세 번째 필드 값이 50보다 큰 줄에서 첫 번째와 두 번째 필드를 출력한다.
2. **내장 변수 사용**
    - **`NR`**: 현재 레코드 번호.
        
        ```bash
        awk '{print NR, $0}' file.txt
        ```
        
    - **`NF`**: 현재 레코드의 필드 개수.
        
        ```bash
        awk '{print $1, NF}' file.txt
        ```
        
3. **사용자 정의 함수**
    
    ```bash
    awk 'function myfunc(x) {return x * x} {print $1, myfunc($2)}' file.txt
    ```
    
    - `myfunc`라는 사용자 정의 함수를 사용하여 두 번째 필드의 제곱을 출력한다.
4. **필드 구분자 변경**
    - **입력 필드 구분자 (`F` 옵션)**
        
        ```bash
        awk -F, '{print $1, $2}' file.csv
        ```
        
    - **출력 필드 구분자 (`OFS` 변수)**
        
        ```bash
        awk -F, 'BEGIN {OFS=" - "} {print $1, $2}' file.csv
        ```
        
5. **정렬된 데이터 출력**
    
    ```bash
    awk '{print $1, $2 | "sort"}' file.txt
    ```
    
    - `awk`로 출력된 데이터를 `sort` 명령어에 파이프하여 정렬된 결과를 출력한다.

### 종합 예제

1. **로그 파일에서 에러 메시지 개수 세기 (`grep`과 `wc` 사용)**
    
    ```bash
    grep -i 'error' /var/log/syslog | wc -l
    ```
    
2. **CSV 파일에서 특정 열의 평균 계산 (`awk` 사용)**
    
    ```bash
    awk -F',' '{sum += $3; count++} END {print sum/count}' data.csv
    ```
    
3. **파일의 특정 패턴 줄 삭제 (`sed` 사용)**
    
    ```bash
    sed '/pattern/d' file.txt
    ```
    
4. **파일에서 여러 패턴을 동시에 검색 (`grep` 사용)**
    
    ```bash
    grep -E 'pattern1|pattern2' file.txt
    ```
    
[[번외] 정규 표현식](regex.md)