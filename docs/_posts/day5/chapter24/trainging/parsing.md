## 실습 

* 제공된 파일은 `data/` 디렉토리에 존재
* 아래 명령어 도구들을 적극 활용할 것: `awk`, `sed`, `cut`, `grep`, `wc`, `sort`, `uniq`

| 번호 | 포맷           | 실습 주제                  | 파일명                  |
| -- | ------------ | ---------------------- | -------------------- |
| 1  | FASTQ        | 품질 점수가 낮은 read 필터링     | `data/ex01.fastq`    |
| 2  | FASTQ        | 특정 시퀀스 motif 찾기        | `data/ex02.fastq`    |
| 3  | VCF          | 특정 변이 위치 추출            | `data/ex03.vcf`      |
| 4  | VCF          | QUAL 점수가 높은 변이만 추출     | `data/ex04.vcf`      |
| 5  | GTF          | feature가 "gene"인 라인 추출 | `data/ex05.gtf`      |
| 6  | GTF          | 특정 유전자 ID만 추출          | `data/ex06.gtf`      |
| 7  | FASTQ (gzip) | 압축된 FASTQ 읽기           | `data/ex07.fastq.gz` |
| 8  | VCF          | chromosome별 변이 개수 세기   | `data/ex08.vcf`      |
| 9  | GTF          | strand별 feature 수 세기   | `data/ex09.gtf`      |
| 10 | VCF          | INFO 필드 파싱하여 DP 값 추출   | `data/ex10.vcf`      |

---

## 실습 문제 설명

### 1. 품질 점수가 낮은 read 필터링

* 파일: `data/ex01.fastq`
* 조건: quality score에 특수문자(`!`, `'`, `*`)가 너무 많은 경우 제외
* 명령어 예시: `awk`, `grep`, `paste`, `cut`

### 2. 특정 시퀀스 motif 찾기

* 파일: `data/ex02.fastq`
* 조건: 시퀀스 라인에 `GATTACA` motif가 있는 read만 출력
* 명령어 예시: `awk 'NR % 4 == 2 && /GATTACA/'`

### 3. 특정 변이 위치 추출

* 파일: `data/ex03.vcf`
* 조건: `chr1`의 `POS=123456`인 행만 출력
* 명령어 예시: `awk '$1 == "chr1" && $2 == 123456'`

### 4. QUAL 점수가 높은 변이만 추출

* 파일: `data/ex04.vcf`
* 조건: QUAL > 30
* 명령어 예시: `awk '!/^#/ && $6 > 30'`

### 5. feature가 "gene"인 라인 추출

* 파일: `data/ex05.gtf`
* 조건: 3번째 필드가 "gene"
* 명령어 예시: `awk '$3 == "gene"'`

### 6. 특정 유전자 ID만 추출

* 파일: `data/ex06.gtf`
* 조건: gene\_id가 "GENE1"인 라인
* 명령어 예시: `awk '$9 ~ /GENE1/'`

### 7. 압축된 FASTQ 읽기

* 파일: `data/ex07.fastq.gz`
* 조건: 압축 해제하지 않고 2개 read 추출
* 명령어 예시: `zcat data/ex07.fastq.gz | head -n 8`

### 8. chromosome별 변이 개수 세기

* 파일: `data/ex08.vcf`
* 조건: 헤더 제외, 1번째 필드 기준으로 개수 세기
* 명령어 예시: `awk '!/^#/ {print $1}' | sort | uniq -c`

### 9. strand별 feature 수 세기

* 파일: `data/ex09.gtf`
* 조건: strand 필드 (+ 또는 -) 기준으로 집계
* 명령어 예시: `awk '{print $7}' | sort | uniq -c`

### 10. INFO 필드 파싱하여 DP 값 추출

* 파일: `data/ex10.vcf`
* 조건: INFO 필드에서 DP=값 만 추출
* 명령어 예시: `awk -F"DP=" '{print $2}' | cut -d";" -f1`

---

## 실습 팁

* `.fastq.gz` 파일은 `zcat`, `zgrep` 등으로 처리 가능

  ```bash
  zcat data/ex07.fastq.gz | head -n 8
  ```
* VCF는 `bcftools`, GTF는 `gffread` 도구로 검증 가능
* 실습 중 필요한 명령어:

  * `awk '{...}'`, `grep 'pattern'`, `cut -f`, `sort`, `uniq`, `head`, `tail`
  * `zcat`, `less`, `wc -l`

