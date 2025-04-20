# [번외] 정규 표현식

- 텍스트 검색, 매칭, 조작을 위한 강력한 도구
- 다양한 유틸리티와 함께 사용되며, 텍스트 파일에서 패턴을 검색하거나 변환하는 데 널리 사용된다.
- 리눅스에서 정규 표현식을 사용하여 텍스트를 처리하는 주요 명령어로는 `grep`, `sed`, `awk` 등이 있다.

### 정규 표현식 기본

1. **문자 매칭**
    - `.`: 임의의 한 문자와 매칭.
        
        ```bash
        grep 'a.b' file.txt
        ```
        
        - 'a'와 'b' 사이에 임의의 한 문자가 있는 패턴을 검색.
2. **문자 클래스**
    - `[]`: 대괄호 안의 문자 중 하나와 매칭.
        
        ```bash
        grep '[aeiou]' file.txt
        ```
        
        - 파일에서 모음(a, e, i, o, u)이 포함된 줄을 검색.
    - `[^]`: 대괄호 안에 없는 문자와 매칭.
        
        ```bash
        grep '[^0-9]' file.txt
        ```
        
        - 숫자가 아닌 문자가 포함된 줄을 검색.
3. **반복**
    - ``: 0번 또는 그 이상 반복.
        
        ```bash
        grep 'fo*' file.txt
        ```
        
        - 'f' 다음에 'o'가 0번 이상 반복되는 패턴을 검색.
    - `+`: 1번 또는 그 이상 반복 (일반적으로 `grep`에서는 `E` 옵션을 사용해야 함).
        
        ```bash
        grep -E 'fo+' file.txt
        ```
        
        - 'f' 다음에 'o'가 1번 이상 반복되는 패턴을 검색.
    - `?`: 0번 또는 1번 반복.
        
        ```bash
        grep -E 'fo?' file.txt
        ```
        
        - 'f' 다음에 'o'가 0번 또는 1번 나오는 패턴을 검색.
    - `{}`: 특정 횟수 반복.
        
        ```bash
        grep -E 'o{2}' file.txt
        ```
        
        - 'o'가 정확히 2번 반복되는 패턴을 검색.
4. **위치**
    - `^`: 행의 시작.
        
        ```bash
        grep '^Hello' file.txt
        ```
        
        - 'Hello'로 시작하는 줄을 검색.
    - `$`: 행의 끝.
        
        ```bash
        grep 'World$' file.txt
        ```
        
        - 'World'로 끝나는 줄을 검색.

### 정규 표현식을 사용하는 리눅스 명령어

### `grep`

1. **기본 사용법**
    
    ```bash
    grep 'pattern' file.txt
    ```
    
2. **확장된 정규 표현식 사용 (`E` 옵션)**
    
    ```bash
    grep -E 'pattern' file.txt
    ```
    
3. **대소문자 구분 없이 검색 (`i` 옵션)**
    
    ```bash
    grep -i 'pattern' file.txt
    ```
    
4. **행 번호 포함 출력 (`n` 옵션)**
    
    ```bash
    grep -n 'pattern' file.txt
    ```
    

### `sed`

1. **기본 사용법**
    
    ```bash
    sed 's/pattern/replacement/' file.txt
    ```
    
2. **파일 내 모든 패턴 교체**
    
    ```bash
    sed 's/pattern/replacement/g' file.txt
    ```
    
3. **여러 패턴을 동시에 교체**
    
    ```bash
    sed -e 's/pattern1/replacement1/' -e 's/pattern2/replacement2/' file.txt
    ```
    

### `awk`

1. **기본 사용법**
    
    ```bash
    awk '/pattern/ {print $0}' file.txt
    ```
    
2. **정규 표현식과 함께 필드 사용**
    
    ```bash
    awk '$1 ~ /pattern/ {print $0}' file.txt
    ```
    
3. **정규 표현식으로 패턴 매칭**
    
    ```bash
    awk '/pattern/ {print $1, $3}' file.txt
    ```
    

### 예제

1. **모든 이메일 주소 검색**
    
    ```bash
    grep -E '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}' file.txt
    ```
    
2. **특정 단어로 시작하는 줄 삭제 (`sed`)**
    
    ```bash
    sed '/^pattern/d' file.txt
    ```
    
3. **특정 패턴을 포함하는 줄만 출력 (`awk`)**
    
    ```bash
    awk '/pattern/ {print $0}' file.txt
    ```