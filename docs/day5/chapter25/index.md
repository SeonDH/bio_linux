---
title: "25. 파일 다루기 고급"
nav_order: 31
layout: default
---

# 25. 파일 다루기 고급

## 주요 바이오 파일 포맷 소개

### 1. FASTQ 파일

**구조**  
1. `@<ID>`: 시퀀스 식별자  
2. `<sequence>`: DNA 서열 (A, C, G, T)  
3. `+`: 구분자 (ID를 반복해도 무방)  
4. `<quality scores>`: Phred-33 인코딩된 품질 점수 (ASCII 33부터)

**Phred Q-score 해석**  
- ASCII 코드 값 − 33 = 품질 점수(Q)  
- 예: `!`(33) → Q0, `"`(34) → Q1, …, `I`(73) → Q40  

**샘플**  
```text
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAAT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
````

**기본 블록 출력**

```bash
awk 'NR%4==1||NR%4==2' sample.fastq
```



### 2. VCF 파일

**구조**

* `##` 헤더: 메타데이터 (`fileformat`, `INFO`, `FORMAT` 등)
* `#CHROM` 라인: 컬럼명 (`CHROM`, `POS`, `ID`, `REF`, `ALT`, `QUAL`, `FILTER`, `INFO` 등)
* 본문: 변이 레코드

**주요 INFO 태그**

* `DP`: 전체 depth
* `AF`: allele frequency
* `MQ`: mapping quality

**샘플**

```text
##fileformat=VCFv4.2
##INFO=<ID=DP,Number=1,Type=Integer,Description="Read Depth">
#CHROM  POS     ID  REF ALT QUAL FILTER INFO
chr1    123456  .   A   T   29.1 PASS   DP=14;AF=0.50;MQ=60
```

**헤더 제외 주요 칼럼 추출**

```bash
awk '!/^#/ { print $1, $2, $4, $5, $6, $8 }' sample.vcf
```


### 3. GTF 파일

**구조 (9개 필드)**

1. `seqname` (chromosome)
2. `source` (annotation 제공자)
3. `feature` (gene, transcript, exon 등)
4. `start`
5. `end`
6. `score`
7. `strand` (+/−)
8. `frame` (0,1,2 또는 `.`)
9. `attributes` (`key "value";` 쌍)

**샘플**

```text
chr1    HAVANA  gene    11869   14409   .   +   .   gene_id "ENSG00000223972"; transcript_id "ENST00000456328";
```

**기본 필드 추출**

```bash
cut -f1,3,9 sample.gtf
```

**특정 유전자(gene\_id)만 추출**

```bash
grep 'gene_id "ENSG00000223972"' sample.gtf \
  | awk '{ print $1, $4, $5, $9 }'
```


## [실습] 파일 다루기

* [[실습] 파일 다루기](training/parsing.md)
