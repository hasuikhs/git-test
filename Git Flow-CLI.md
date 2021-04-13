# Git Flow

> - 브랜치를 쉽게 사용 가능하게 구현해 놓은 git 확장
> - Git 브랜치 전략

<img src="Git_Flow.assets/git-model@2x.png" alt="img" style="zoom: 50%;" />

## 1. 설치

- Window는 `git for window` 에 이미 포함

- Ubuntu

  ```bash
  $ apt-get install git-flow
  ```

## 2. 사용

- 브랜치를 관리할 로컬 저장소 디렉토리에서 시작

  ```bash
  $ git flow init
  
  # 기본 브랜치 생성하기
  $ git flow init -d
  
  # 브랜치 목록을 가져오고 git flow 전략에 맞게 다시 설정하고 싶다면
  $ git flow init -f
  ```

### 2.1 git flow branch 종류

#### 2.1.1 master

- 배포될 안정적인 최신 버전의 소스코드가 있는 브랜치
- **master 브랜치에는 배포해도 될 만큼 안정성이 검증된 코드들이 병합됨**

#### 2.1.2 develop

- 끊임 없이 새로운 기능들과 버그 수정들이 병합됨
- 개발자들은 develop 브랜치를 기준으로 feature 브랜치를 생성 후 작업한다음 병합함

#### 2.1.3 feature

- 새로운 기능 개발을 위해 생성하는 브랜치
- **기능 개발이 완료된 다음 `git flow finish` 되면 develop에 병합 후 브랜치는 삭제**

#### 2.1.4 release

- 새로운 release를 생성하기 위해 만들어지는 브랜치
- **develop 브랜치를 기반으로 생성되며 develop 브랜치와 master 브랜치로 병합**
- release 브랜치에는 릴리즈 준비 과정에서 발견된 **버그 수정 사항 같은 패치들만 적용**
- **release 브랜치가 안정적이라 판단되면 master브랜치에 병합**
- release 브랜치에 수정된 버그들은 develop 브랜치로도 다시 병합

#### 2.1.5 hotfix

- **긴급하게 수행되어야 할 버그 수정을 반영하기 위해 생성되는 브랜치**
- **master 브랜치를 기반으로 생성**
- master 브랜치로 병합되고, develop 브랜치로도 병합

### 2.2 시나리오

#### 2.2.1 feature 사용

- git flow 시작

  ```bash
  $ git flow init
  ```

- 기능 개발을 위해 feature 하위 브랜치 생성

  ```bash
  (develop)$  git flow feature start <feature_name>
  ```

- 기능 개발 후

  ```bash
  (feature/<feature_name>)$ git add <edit file>
  
  (feature/<feature_name>)$ git commit -m "<commit comment>"
  
  # finish되면 현재 feature 브랜치는 삭제되고 develop에 병합
  (feature/<feature_name>)$ git flow feature finish <feature_name>
  
  # develop 브랜치로 checkout 됨
  (develop)$ git push origin develop
  ```

#### 2.2.2 feature 개발 중에 누군가 필요로 하는 경우

- commit 이후

  ```bash
  # publish 하면 remote 저장소로 현재 feature 브랜치 이름으로 업로드 됨
  (feature/<feature_name>)$ git flow feature publish <feature_name>
  ```

- 다른 사용자의 변경 내용을 가져오기

  ```bash
  # remote 저장소에서 위의 feature 브랜치 가져오기
  $ git flow feature pull origin <feature_name>
  ```

#### 2.2.3 release 사용

- 기본적으로 feature 와 비슷

  ```bash
  $ git flow release start <version>
  
  $ git flow release publish <version>
  ```

- 하지만 `pull` 대신 `track` 사용

  ```bash
  $ git flow release track <version>
  ```

- release finish

  ```bash
  # release 브랜치를 master, develop 브랜치에 병합
  # release 버전을 태그로 생성하고, git flow init에서 명시한 version tag prefix 문자열이 release 버전 앞에 추가
  $ git flow release finish <version>
  
  # 새로운 release가 포함된 master 브랜치를 remote 저장소에 태그와 함께 push
  $ git push --tags
  ```

#### 2.2.4 hotfix 사용

```bash
$ git flow hotfix start <version>

# hotfix 브랜치를 master, develop 브랜치에 병합
# hotfix 버전을 태그로 생성하고, git flow init에서 명시한 version tag prefix 문자열이 hotfix 버전 앞에 추가
$ git flow hotfix finish <version>

$ git push \--tags
```

