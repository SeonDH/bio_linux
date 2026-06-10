# [실습] Conda 환경 변수 설정 방법 비교 - 15분

이 실습에서는 Conda 환경에 변수를 설정하는 두 가지 방법을 비교한다.

1. `environment.yml`의 `variables` 항목을 사용하는 방법
2. 환경 활성화 시 실행되는 `activate.d` 스크립트를 사용하는 방법

## 실습 전 준비

Miniconda 설치와 `conda` 명령어 등록이 끝난 상태에서 진행한다.

```bash
conda --version
```

### 확인용 스크립트 작성

```bash
mkdir -p ~/conda_practice
cd ~/conda_practice
vi check_env.sh
```

아래 내용을 입력한다.

```bash
#!/bin/bash
echo "현재 Conda 환경: $CONDA_DEFAULT_ENV"
echo "BIO_PROJECT: $BIO_PROJECT"
```

실행 권한을 부여한다.

```bash
chmod +x check_env.sh
```

## 실습 문제

1. `environment.yml`을 이용해 `bio_env_yaml` 환경을 만든다.
    - 환경 변수 `BIO_PROJECT` 값은 `YAML`로 설정한다.
    - `conda-forge` 채널에서 `figlet` 패키지가 설치되도록 설정한다.

2. `bio_env_yaml` 환경을 활성화하고 `check_env.sh`를 실행해 결과를 확인한다.

3. `bio_env_yaml` 환경에서 `figlet CONDA` 명령어가 실행되는지 확인한다.

4. `bio_env_script`라는 Conda 환경을 만든다.

5. `bio_env_script`를 활성화했을 때 `BIO_PROJECT` 값이 `SCRIPT`가 되도록 설정한다.

6. `bio_env_script` 환경을 활성화하고 `check_env.sh`를 실행해 결과를 확인한다.

7. Conda 환경을 비활성화한 뒤 `check_env.sh`를 다시 실행해 차이를 확인한다.

8. 두 방법의 차이를 간단히 정리해본다.

9. 실습이 끝나면 `bio_env_yaml`, `bio_env_script` 환경을 삭제한다.

> 힌트: `environment.yml` 방식은 환경을 만들 때 변수와 설치할 패키지를 함께 정의한다. `activate.d` 방식은 환경이 활성화될 때 실행할 스크립트를 `~/miniconda3/envs/{환경이름}/etc/conda/activate.d/` 아래에 둔다.

## 답지

- [답지 예시](../solution/conda_env_variable_solution.md)
