# [번외] Git Flow

# Git Flow

### 개요

Git Flow는 Vincent Driessen이 2010년에 제안한 Git 브랜치 모델로, 소프트웨어 개발에서 체계적인 버전 관리를 위해 설계되었다. Git Flow는 명확한 브랜치 구조와 작업 흐름을 제공하여, 팀 협업과 릴리즈 관리가 용이하도록 돕는다.

### Git Flow 브랜치 모델

Git Flow는 다음과 같은 주요 브랜치로 구성된다:

1. **main (또는 master) 브랜치**
    - 배포 가능한 상태의 코드가 저장되는 브랜치이다.
    - 항상 안정적인 버전을 유지하며, 실제 배포되는 코드는 이 브랜치에 있다.
2. **develop 브랜치**
    - 기능 개발이 이루어지는 브랜치이다.
    - 이 브랜치는 다음 릴리즈를 준비하는 모든 기능이 통합되는 곳이다.
3. **feature 브랜치**
    - 새로운 기능을 개발할 때 사용하는 브랜치이다.
    - 각 기능은 별도의 feature 브랜치에서 개발되며, 완료되면 develop 브랜치로 병합된다.
    - 이름은 `feature/기능명` 형식을 사용한다.
4. **release 브랜치**
    - 릴리즈 준비를 위해 사용하는 브랜치이다.
    - develop 브랜치에서 분기하여 버그 수정, 문서 작성, 최종 테스트 등을 진행한다.
    - 이름은 `release/버전명` 형식을 사용한다.
    - 준비가 완료되면 main 브랜치로 병합되고, 다시 develop 브랜치로 병합된다.
5. **hotfix 브랜치**
    - 배포된 버전에서 발생한 긴급한 버그를 수정할 때 사용하는 브랜치이다.
    - main 브랜치에서 분기하여 버그를 수정하고, 수정이 완료되면 main 브랜치와 develop 브랜치로 병합된다.
    - 이름은 `hotfix/버그명` 형식을 사용한다.

### Git Flow 작업 흐름


<img src="../images/Untitled 4.png" width="60%">


1. **기능 개발 (Feature Branch)**
    - 새로운 기능을 추가하기 위해 develop 브랜치에서 feature 브랜치를 생성한다.
        
        ```
        git checkout develop
        git checkout -b feature/새로운기능
        ```
        
    - 기능 개발을 완료한 후, develop 브랜치로 병합한다.
        
        ```
        git checkout develop
        git merge feature/새로운기능
        git branch -d feature/새로운기능
        ```
        
2. **릴리즈 준비 (Release Branch)**
    - 새로운 릴리즈를 준비하기 위해 develop 브랜치에서 release 브랜치를 생성한다.
        
        ```
        git checkout develop
        git checkout -b release/버전명
        ```
        
    - 릴리즈 준비 과정에서 버그 수정, 문서 작성 등을 진행하고, 준비가 완료되면 main 브랜치로 병합한다.
        
        ```
        git checkout main
        git merge release/버전명
        git tag -a 버전명
        ```
        
    - 릴리즈 브랜치는 다시 develop 브랜치로 병합된다.
        
        ```
        git checkout develop
        git merge release/버전명
        git branch -d release/버전명
        ```
        
3. **긴급 수정 (Hotfix Branch)**
    - 배포된 버전에서 발생한 긴급한 버그를 수정하기 위해 main 브랜치에서 hotfix 브랜치를 생성한다.
        
        ```
        git checkout main
        git checkout -b hotfix/버그명
        ```
        
    - 버그 수정을 완료한 후, main 브랜치와 develop 브랜치로 병합한다.
        
        ```
        git checkout main
        git merge hotfix/버그명
        git tag -a 버전명
        
        git checkout develop
        git merge hotfix/버그명
        git branch -d hotfix/버그명
        ```
        

### Git Flow의 장점

1. **명확한 브랜치 구조**
    - Git Flow는 명확한 브랜치 구조를 제공하여, 개발자가 현재 작업이 어떤 단계에 있는지 쉽게 파악할 수 있다.
    - 이를 통해 개발, 테스트, 배포 과정이 체계적으로 관리된다.
2. **병행 개발 지원**
    - 여러 개의 feature 브랜치를 통해 여러 기능을 병행 개발할 수 있다.
    - 이를 통해 대규모 프로젝트에서도 효율적으로 작업을 진행할 수 있다.
3. **안정적인 릴리즈 관리**
    - release 브랜치를 통해 릴리즈 준비를 체계적으로 관리할 수 있다.
    - hotfix 브랜치를 통해 긴급한 버그 수정이 필요한 경우에도 안정적인 배포를 유지할 수 있다.
4. **효율적인 협업**
    - Git Flow는 팀 내 협업을 원활하게 하며, 각 개발자의 작업 내용을 명확히 구분하고 관리할 수 있다.
    - 이를 통해 코드 품질을 높이고, 충돌을 최소화할 수 있다.