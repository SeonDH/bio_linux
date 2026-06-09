# [번외] grep, sed, awk 의 고급 사용

`grep`, `sed`, `awk`의 고급 사용법을 익히면 리눅스에서 복잡한 텍스트 처리와 데이터 조작 작업을 매우 효율적으로 수행할 수 있다. 각 명령어의 고급 사용법을 예시와 함께 설명한다.

## 기본 문법 먼저 보기

`grep`, `sed`, `awk`는 모두 텍스트 파일을 줄 단위로 처리하지만 역할이 조금 다르다.

| 명령어 | 주 용도 | 기본 형태 |
| --- | --- | --- |
| `grep` | 특정 패턴이 들어 있는 줄 찾기 | `grep '패턴' 파일` |
| `sed` | 줄 단위로 텍스트 치환, 삭제, 삽입 | `sed '주소명령' 파일` |
| `awk` | 열 단위로 데이터를 필터링하고 출력 | `awk '조건 {동작}' 파일` |

### `sed` 기본 문법

`sed`는 파일을 한 줄씩 읽으면서 지정한 편집 명령을 적용한다.

```bash
sed 's/찾을문자/바꿀문자/' file.txt
```

자주 쓰는 형태는 다음과 같다.

| 문법 | 의미 |
| --- | --- |
| `s/old/new/` | 한 줄에서 처음 만나는 `old`를 `new`로 바꿈 |
| `s/old/new/g` | 한 줄의 모든 `old`를 `new`로 바꿈 |
| `1,3s/old/new/` | 1번 줄부터 3번 줄까지만 치환 |
| `/pattern/d` | `pattern`이 들어 있는 줄 삭제 |
| `2i\text` | 2번 줄 앞에 `text` 삽입 |
| `$a\text` | 파일 마지막 줄 뒤에 `text` 추가 |

예:

```bash
sed 's/apple/APPLE/g' fruits.txt
sed '/banana/d' fruits.txt
```

찾을 문자열이나 바꿀 문자열에 `/`가 많이 들어 있으면 구분자를 다른 문자로 바꿔 쓸 수 있다.

```bash
sed 's#/home/user/data#/data/project#g' paths.txt
sed 's|http://old.example.com|https://new.example.com|g' urls.txt
```

- `s/old/new/g`와 `s#old#new#g`, `s|old|new|g`는 같은 구조이다.
- 경로나 URL처럼 `/`가 많은 문자열을 바꿀 때는 `#` 또는 `|`를 구분자로 쓰면 읽기 쉽다.

> `sed`는 기본적으로 원본 파일을 직접 바꾸지 않고, 바뀐 결과를 화면에 출력한다. 원본 파일을 직접 바꾸려면 `sed -i` 옵션을 사용하지만, 실습에서는 먼저 화면 출력으로 확인한 뒤 사용하는 것이 좋다.

### `awk` 기본 문법

`awk`는 줄을 여러 필드로 나누어 조건에 맞는 줄을 출력하거나 계산할 때 많이 사용한다.

```bash
awk '조건 {동작}' file.txt
```

자주 쓰는 표현은 다음과 같다.

| 문법 | 의미 |
| --- | --- |
| `$1`, `$2`, `$3` | 1번째, 2번째, 3번째 필드 |
| `$0` | 현재 줄 전체 |
| `NR` | 현재 줄 번호 |
| `NF` | 현재 줄의 필드 개수 |
| `-F,` | 입력 구분자를 쉼표로 지정 |
| `BEGIN { ... }` | 파일을 읽기 전에 한 번 실행 |
| `END { ... }` | 파일을 모두 읽은 뒤 한 번 실행 |
| `$3 > 50` | 3번째 필드 값이 50보다 큰 줄 |
| `$2 == "fruit"` | 2번째 필드가 `fruit`인 줄 |
| `$1 ~ /chr1/` | 1번째 필드가 정규 표현식 `chr1`과 매칭되는 줄 |

예:

```bash
awk '{print $1, $3}' data.txt
awk -F, '$2 == "fruit" {print $1, $3}' data.csv
awk '{sum += $2} END {print sum}' data.txt
```

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
