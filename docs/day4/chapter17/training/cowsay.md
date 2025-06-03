# \[번외] cowsay

`cowsay`는 입력한 문자열을 말풍선과 함께 ASCII 아트 형태의 동물이 출력하는 유틸리티 프로그램이다. 기본적으로 소(cow) 형태이지만 다양한 동물 형식도 지원한다.

---

## 1. 기본 사용법

아래 명령어는 소가 지정된 문구를 말풍선으로 출력한다.

```bash
cowsay "패키지 관리 실습 중입니다!"
```

---

## 2. 다른 동물 사용하기

`-f` 옵션을 사용하면 다른 동물 모양으로 출력할 수 있다.

```bash
cowsay -f tux "Hello from Tux!"
```

> `-f` 뒤에는 `/usr/share/cowsay/cows/` 디렉토리에 있는 `.cow` 파일 이름을 지정할 수 있다.

---

## 3. `fortune`과 함께 사용하기

`fortune`은 무작위 명언이나 유머 문구를 출력하는 프로그램이다. `cowsay`와 조합하면 자동으로 재미있는 말풍선이 생성된다.

### 설치:

```bash
sudo apt install fortune
```

### 사용 예:

```bash
fortune | cowsay
```

---

## 참고

* 추가 동물 목록 보기:

```bash
cowsay -l
```

* `cowthink` 명령어를 사용하면 말풍선 대신 생각풍선으로 출력할 수 있다:

```bash
cowthink "이건 생각입니다..."
```