# [번외] 표준 입력과 인자의 차이

### 표준 입력과 인자의 차이

### 차이점

1. **입력 방식**:
    - **표준 입력**: 파일의 내용을 표준 입력 스트림을 통해 프로그램에 전달한다.
    - **인자**: 파일 이름을 명령어의 인자로 전달하여 프로그램이 직접 파일을 읽도록 한다.
2. **파일 이름 인식**:
    - **표준 입력**: 프로그램은 파일 이름을 알지 못한다. 단순히 표준 입력으로 들어오는 데이터를 처리한다.
    - **인자**: 프로그램이 파일 이름을 알 수 있다. 파일 이름을 출력하거나 여러 파일을 한 번에 처리할 수 있다.
3. **여러 파일 처리**:
    - **표준 입력**: 한 번에 하나의 파일만 표준 입력으로 처리할 수 있다.
    - **인자**: 여러 파일을 인자로 전달할 수 있으며, 프로그램이 이를 개별적으로 처리할 수 있다.

### 구체적인 예제

### 1. 파일 이름 출력

**파일 `data.txt`**:

```text
info: starting process
error: failed to start process
info: process running
warning: low memory
error: out of memory
info: process completed
```

### 표준 입력을 사용하는 경우

```bash
grep "error" < data.txt
```

- **설명**: `grep` 명령어는 표준 입력으로 들어오는 `data.txt` 파일의 내용을 읽어서 "error"를 포함하는 줄을 검색한다.
- **결과**:
    
    ```text
    error: failed to start process
    error: out of memory
    ```
    

### 인자를 사용하는 경우

```bash
grep -H "error" data.txt
```

- **설명**: `grep` 명령어는 `data.txt` 파일을 직접 읽어서 "error"를 포함하는 줄을 검색하고, 파일 이름과 함께 출력한다.
- **결과**:
    
    ```text
    data.txt:error: failed to start process
    data.txt:error: out of memory
    ```
    

### 2. 여러 파일 처리

**파일 `file1.txt`**:

```text
info: process running
error: file not found
```

**파일 `file2.txt`**:

```text
warning: disk space low
error: unable to read file
```

### 표준 입력을 사용하는 경우

```bash
cat file1.txt file2.txt | grep "error"
```

- **설명**: `cat` 명령어는 `file1.txt`와 `file2.txt`의 내용을 표준 입력으로 합친다. `grep` 명령어는 이 합쳐진 내용에서 "error"를 포함하는 줄을 검색한다.
- **결과**:
    
    ```text
    error: file not found
    error: unable to read file
    ```
    

### 인자를 사용하는 경우

```bash
grep "error" file1.txt file2.txt
```

- **설명**: `grep` 명령어는 `file1.txt`와 `file2.txt`를 직접 읽어서 "error"를 포함하는 줄을 검색하고, 각 줄의 앞에 해당 파일 이름을 함께 출력한다.
- **결과**:
    
    ```text
    file1.txt:error: file not found
    file2.txt:error: unable to read file
    ```