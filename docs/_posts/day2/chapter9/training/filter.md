# [실습] 필터 - 10분

## 실습 전 명령어

```bash
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

---

## 실습 문제

1. **"cat"을 포함하는 모든 줄을 출력하자**  
   - 힌트: `grep` 명령어를 사용해 특정 문자열이 포함된 줄을 찾는다.

2. **"mammal"을 "MAMMAL"로 치환하여 출력하자**  
   - 힌트: `sed` 명령어에서 `s/old/new/g` 패턴을 사용해 치환한다.

3. **첫 번째 필드만 출력하자**  
   - 힌트: `awk -F,` 또는 `cut -d, -f1` 명령어를 사용할 수 있다.

4. **정렬해서 출력하자**  
   - 힌트: `sort` 명령어를 사용하여 알파벳순 정렬을 수행한다.

