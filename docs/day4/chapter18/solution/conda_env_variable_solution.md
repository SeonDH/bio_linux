# [답지] Conda 환경 변수 설정 방법 비교

## 1. Conda 설치 확인

```bash
conda --version
```

## 2. 확인용 스크립트 작성

```bash
mkdir -p ~/conda_practice
cd ~/conda_practice
vi check_env.sh
```

입력 내용:

```bash
#!/bin/bash
echo "현재 Conda 환경: $CONDA_DEFAULT_ENV"
echo "BIO_PROJECT: $BIO_PROJECT"
```

실행 권한 부여:

```bash
chmod +x check_env.sh
```

## 3. `environment.yml` 방식

```bash
vi environment.yml
```

입력 내용:

```yaml
name: bio_env_yaml
channels:
  - conda-forge
dependencies:
  - figlet
variables:
  BIO_PROJECT: "YAML"
```

환경 생성:

```bash
conda env create -f environment.yml
```

확인:

```bash
conda activate bio_env_yaml
./check_env.sh
```

예상 결과:

```text
현재 Conda 환경: bio_env_yaml
BIO_PROJECT: YAML
```

`dependencies`에 적은 `figlet`이 설치되었는지 확인한다.

```bash
figlet CONDA
```

## 4. `activate.d` 스크립트 방식

```bash
conda create -n bio_env_script -y
mkdir -p ~/miniconda3/envs/bio_env_script/etc/conda/activate.d
echo 'export BIO_PROJECT="SCRIPT"' > ~/miniconda3/envs/bio_env_script/etc/conda/activate.d/env_vars.sh
chmod +x ~/miniconda3/envs/bio_env_script/etc/conda/activate.d/env_vars.sh
```

확인:

```bash
conda activate bio_env_script
./check_env.sh
```

예상 결과:

```text
현재 Conda 환경: bio_env_script
BIO_PROJECT: SCRIPT
```

## 5. 비활성화 후 확인

```bash
conda deactivate
./check_env.sh
```

비활성화 후에는 `CONDA_DEFAULT_ENV`와 `BIO_PROJECT` 값이 비어 있을 수 있다.

## 6. 두 방법의 차이

- `environment.yml` 방식: 환경을 파일로 정의하고 다시 만들기 쉽다.
- `dependencies` 항목: 환경을 만들 때 설치할 패키지를 함께 적을 수 있다.
- `channels` 항목: 패키지를 받을 저장소를 지정한다. 이 예시에서는 `figlet` 설치를 위해 `conda-forge`를 사용한다.
- `activate.d` 방식: 환경이 활성화될 때 실행할 명령을 직접 넣을 수 있어 더 유연하다.

## 7. 실습 환경 정리

```bash
conda remove -n bio_env_yaml --all -y
conda remove -n bio_env_script --all -y
```
