# [실습] Docker 배치 파이프라인 - 30분

이 실습은 로컬 Linux에서 진행한다. 실제 유전체 데이터나 전문 바이오 분석 툴은 사용하지 않고, 미리 준비된 가상 텍스트 파일을 분석 데이터로 가정한다.

## 목표

1. Docker 컨테이너를 일회성 분석 작업처럼 실행한다.
2. `-v` 옵션으로 호스트의 입력/출력 디렉터리를 컨테이너에 연결한다.
3. `--rm` 옵션으로 작업 종료 후 컨테이너를 자동 삭제한다.
4. 결과 파일만 호스트 디렉터리에 남기는 구조를 확인한다.

## 1. 실습 디렉터리 준비

```bash
mkdir -p ~/docker_batch/input ~/docker_batch/output
cd ~/docker_batch
```

## 2. 실습 데이터 준비

교재 저장소를 로컬에 받아둔 상태라면, 저장소 루트에서 아래 명령어로 복사한다.

```bash
cp docs/day5/chapter22/data/mock_data.txt ~/docker_batch/input/mock_data.txt
```

데이터 일부를 확인한다.

```bash
head input/mock_data.txt
wc -l input/mock_data.txt
```

## 3. 분석 스크립트 작성

`run_pipeline.sh` 파일을 만든다.

```bash
vi run_pipeline.sh
```

아래 내용을 입력한다.

```bash
#!/bin/sh
set -eu

INPUT_FILE="${1:-/data/input/mock_data.txt}"
OUTPUT_DIR="${2:-/data/output}"
KEYWORD="${3:-gene_1}"

mkdir -p "$OUTPUT_DIR"

echo "Input file: $INPUT_FILE"
echo "Output dir: $OUTPUT_DIR"
echo "Keyword: $KEYWORD"

wc -l "$INPUT_FILE" > "$OUTPUT_DIR/line_count.txt"
awk -v keyword="$KEYWORD" '$2 == keyword' "$INPUT_FILE" > "$OUTPUT_DIR/matched_lines.txt"
wc -l "$OUTPUT_DIR/matched_lines.txt" > "$OUTPUT_DIR/match_count.txt"

awk '{ print $2 }' "$INPUT_FILE" \
  | sort \
  | uniq -c \
  | sort -nr \
  > "$OUTPUT_DIR/gene_summary.txt"

echo "Pipeline finished."
```

실행 권한을 부여한다.

```bash
chmod +x run_pipeline.sh
```

## 4. Dockerfile 작성

`Dockerfile` 파일을 만든다.

```bash
vi Dockerfile
```

아래 내용을 입력한다.

```dockerfile
FROM alpine:latest

WORKDIR /pipeline

COPY run_pipeline.sh .
RUN chmod +x run_pipeline.sh

ENTRYPOINT ["./run_pipeline.sh"]
```

## 5. 이미지 빌드

```bash
docker build -t bio-batch-demo:latest .
```

이미지가 생성되었는지 확인한다.

```bash
docker images
```

## 6. 컨테이너 실행

입력 디렉터리와 출력 디렉터리를 컨테이너 안의 `/data/input`, `/data/output`에 연결한다.

```bash
docker run --rm \
  -v "$PWD/input:/data/input:ro" \
  -v "$PWD/output:/data/output" \
  bio-batch-demo:latest
```

옵션의 의미는 다음과 같다.

| 옵션 | 의미 |
| --- | --- |
| `--rm` | 컨테이너 종료 후 컨테이너를 자동 삭제 |
| `-v "$PWD/input:/data/input:ro"` | 호스트의 `input` 디렉터리를 컨테이너에 읽기 전용으로 연결 |
| `-v "$PWD/output:/data/output"` | 호스트의 `output` 디렉터리를 컨테이너에 읽기/쓰기 가능하게 연결 |
| `bio-batch-demo:latest` | 실행할 Docker 이미지 |

## 7. 결과 확인

컨테이너는 종료되었지만 결과 파일은 호스트의 `output` 디렉터리에 남아 있다.

```bash
ls -lh output
cat output/line_count.txt
cat output/match_count.txt
head output/gene_summary.txt
```

## 8. 검색 키워드 바꿔 실행하기

컨테이너 실행 시 인자를 전달하면 다른 키워드로 분석할 수 있다.

```bash
docker run --rm \
  -v "$PWD/input:/data/input:ro" \
  -v "$PWD/output:/data/output" \
  bio-batch-demo:latest \
  /data/input/mock_data.txt /data/output gene_7
```

결과를 다시 확인한다.

```bash
cat output/match_count.txt
head output/matched_lines.txt
```

## 9. 자원 제한을 포함한 실행

로컬 Linux에서도 컨테이너가 사용할 CPU와 메모리를 제한할 수 있다.

```bash
docker run --rm \
  --cpus=2 \
  --memory=2g \
  -v "$PWD/input:/data/input:ro" \
  -v "$PWD/output:/data/output" \
  bio-batch-demo:latest
```

## 정리

이 실습은 컨테이너 기반 배치 분석에서 이해해야 할 기본 실행 패턴을 다룬다. 컨테이너는 분석 환경과 실행 스크립트를 제공하고, 실제 데이터와 결과물은 호스트 디렉터리에 남긴다.

## 답지

- [답지 예시](../solution/batch_pipeline_solution.md)
