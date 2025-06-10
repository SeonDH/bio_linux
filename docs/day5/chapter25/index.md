---
title: "25. 파일 다루기 고급"
nav_order: 31
layout: default
---


# 25. 파일 다루기 고급

## 주요 바이오 파일 포맷 소개

### 1. FASTQ 파일

* DNA 시퀀싱 결과를 표현하는 텍스트 포맷
* 4줄 단위로 구성: `@ID`, `sequence`, `+`, `quality score`

#### [시연 예제] fastq 예시 파일

```text
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAAT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
```

#### `awk`로 FASTQ 레코드 블록 출력

```bash
awk 'NR % 4 == 1 || NR % 4 == 2' sample.fastq
```


### 2. VCF 파일

* 변이 정보를 담는 포맷 (variant call format)
* 헤더(`##`, `#CHROM`), 본문 (변이 정보)

#### [시연 예제] vcf 예시 파일

```text
##fileformat=VCFv4.2
#CHROM	POS	ID	REF	ALT	QUAL	FILTER	INFO
chr1	123456	.	A	T	29.1	PASS	.
```

#### `awk` 시연 예제

```bash
awk '!/^#/ { print $1, $2, $4, $5 }' sample.vcf
```


### 3. GTF 파일

* 유전자 주석 정보 표현
* 필드: chrom, source, feature, start, end, score, strand, frame, attributes

#### [시연 예제] gtf 예시 파일

```text
chr1	HAVANA	gene	11869	14409	.	+	.	gene_id "ENSG00000223972";
```

#### `cut` 시연 예제

```bash
cut -f1,3,9 sample.gtf
```

## [실습] 파일 다루기

- [[실습] 파일 다루기](trainging/parsing.md)

