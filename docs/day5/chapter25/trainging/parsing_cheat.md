## 실습 문제 답지

### 1. 품질 점수가 낮은 read 필터링

```bash
awk 'NR%4==0 && ($0 ~ /[!*'\''"]/)' data/ex01.fastq
```

> 출력된 라인에 해당하는 read 1개(총 4줄)를 제거하는 스크립트로 확장 가능


### 2. 특정 시퀀스 motif 찾기

```bash
awk 'NR%4==2 && /GATTACA/' data/ex02.fastq
```


### 3. 특정 변이 위치 추출

```bash
awk '$1=="chr1" && $2==123456' data/ex03.vcf
```


### 4. QUAL 점수가 높은 변이만 추출

```bash
awk '!/^#/ && $6 > 30' data/ex04.vcf
```


### 5. feature가 "gene"인 라인 추출

```bash
awk '$3 == "gene"' data/ex05.gtf
```


### 6. 특정 유전자 ID만 추출

```bash
awk '$9 ~ /gene_id "GENE1"/' data/ex06.gtf
```


### 7. 압축된 FASTQ 읽기

```bash
zcat data/ex07.fastq.gz | head -n 8
```


### 8. chromosome별 변이 개수 세기

```bash
awk '!/^#/ {print $1}' data/ex08.vcf | sort | uniq -c
```


### 9. strand별 feature 수 세기

```bash
awk '{print $7}' data/ex09.gtf | sort | uniq -c
```


### 10. INFO 필드 파싱하여 DP 값 추출

```bash
awk -F"\t" '!/^#/ { split($8,a,";"); for(i in a) if(a[i] ~ /^DP=/) print a[i] }' data/ex10.vcf | cut -d"=" -f2
```