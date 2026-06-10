# [답지] 파이프라인과 필터

## 1. 중복 제거 후 역순 정렬

```bash
sort animals.txt | uniq | sort -r
```

## 2. `mammal` 줄에서 첫 번째 필드만 출력

```bash
grep "mammal" animals.txt | cut -d, -f1
```

## 3. 출현 횟수 상위 3개 동물명 출력

```bash
cut -d, -f1 animals.txt | sort | uniq -c | sort -nr | head -n 3
```
