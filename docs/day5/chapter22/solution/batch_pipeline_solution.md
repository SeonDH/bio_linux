# [답지] Docker 배치 파이프라인

## 1. 실습 디렉터리와 입력 파일 확인

```bash
mkdir -p ~/docker_batch/input ~/docker_batch/output
cd ~/docker_batch
cp docs/day5/chapter22/data/mock_data.txt ~/docker_batch/input/mock_data.txt
head input/mock_data.txt
wc -l input/mock_data.txt
```

## 2. 분석 스크립트 작성

```bash
vi run_pipeline.sh
```

입력 내용:

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

```bash
chmod +x run_pipeline.sh
```

## 3. Dockerfile 작성

```bash
vi Dockerfile
```

입력 내용:

```dockerfile
FROM alpine:latest

WORKDIR /pipeline

COPY run_pipeline.sh .
RUN chmod +x run_pipeline.sh

ENTRYPOINT ["./run_pipeline.sh"]
```

## 4. 이미지 빌드와 실행

```bash
docker build -t bio-batch-demo:latest .
docker run --rm \
  -v "$PWD/input:/data/input:ro" \
  -v "$PWD/output:/data/output" \
  bio-batch-demo:latest
```

## 5. 결과 확인

```bash
ls -lh output
cat output/line_count.txt
cat output/match_count.txt
head output/gene_summary.txt
```

## 6. 키워드 변경 실행

```bash
docker run --rm \
  -v "$PWD/input:/data/input:ro" \
  -v "$PWD/output:/data/output" \
  bio-batch-demo:latest \
  /data/input/mock_data.txt /data/output gene_7
```

```bash
cat output/match_count.txt
head output/matched_lines.txt
```
