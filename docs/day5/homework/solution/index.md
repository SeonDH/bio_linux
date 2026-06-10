# Day 5 과제 답지 예시

## 셸 스크립트 복습

```bash
vi review.sh
```

입력 내용:

```bash
#!/bin/bash
echo "현재 사용자: $USER"
echo "현재 위치:"
pwd
echo "현재 시간:"
date
```

실행:

```bash
chmod +x review.sh
./review.sh
```

## 파일 다루기 복습

```bash
mkdir -p day5_review
cd day5_review

echo "sample1" > sample.txt
echo "sample2" >> sample.txt
echo "sample3" >> sample.txt

cp sample.txt sample_copy.txt
mv sample_copy.txt sample_backup.txt
wc sample.txt
grep "sample2" sample.txt
```
