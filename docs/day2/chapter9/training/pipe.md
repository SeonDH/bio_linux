
# [실습] 파이프라인과 필터 - 10분

## 실습 전 준비

```
cat <<EOL > animals.txt
dog,mammal,4
cat,mammal,4
sparrow,bird,2
goldfish,fish,0
cat,mammal,4
dog,mammal,4
parrot,bird,2
dolphin,mammal,0
goldfish,fish,0
sparrow,bird,2
parrot,bird,2
EOL
```

## 실습 문제

1. 중복된 줄을 제거한 후, 알파벳 역순으로 정렬하여 출력하세요.

    힌트: sort, uniq, -r 옵션

2. 'mammal'이 포함된 줄만 추출한 뒤, 필드 구분자를 기준으로 첫 번째 필드만 출력하세요.

    힌트: grep, cut -d',' -f1

3. 출현 횟수가 많은 동물명을 기준으로 정렬하여 상위 3개만 출력하세요.

    힌트: cut, sort, uniq -c, sort -nr, head

