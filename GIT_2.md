## GIT_2

## 1. Branch

- 독립적으로 어떤 작업을 진행하기 위한 개념
- 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않아
- 여러 작업을 동시에 진행이 가능

### 1.1 branch 만들기

   ```bash
   $ git branch <branch name>
   ```

### 1.2 branch 전환하기

   ```bash
   $ git checkout <branch name>
   
   // 브랜치 만들기와 체크아웃을 한번에 하는 방법
   $ git checkout -b <branch name>
   ```

### 1.3 branch 병합하기

   ```bash
   // 다른 branch로 checkout 된 상태에서 
   // 즉, 다른 branch에서 add 와 commit을 한 후에
   // 다시 master branch로 checkout
   $ git merge <branch name>
   
   // 충돌 발생시 해당 파일의 코드로 이동하여 해결 후 add와 commit
   ```

### 1.4 branch 삭제하기

   ```bash
   // 다른 branch의 내용이 모두 master로 통합되었기에 필요하지가 않다
   $ git branch -d <branch name>
   ```


## 2. 기타 명령어

   - 파일 삭제

     ```bash
     $ git rm --cashed --ignore-unmatch 파일명
     ```

   - 히스토리 삭제

     - 목적 : 비밀번호, api키 같은 비공개 정보가 담긴 파일을 실수로 올렸을때 삭제하는 방법

     ```bash
     $ git clone http://github 주소	# 소스 다운로드
     $ cd 폴더명/	# 폴더 이동
     $ git filter-branch --index-filter 'git rm --cashed --ignore-unmatch 파일명' --prune-empty -- --all # 모든 히스토리에서 해당 파일 삭제
     $ git push origin master --force # 서버로 전송
     ```

   - 히스토리에서 폴더 삭제

     ```bash
     $ git filter-branch --tree-filter 'rm -rf vendor/gems' HEAD
     ```

   - 원격 저장소 추가하여 로컬에 싱크하기

     ```bash
     $ git remote add upstream http://github 주소
     $ git pull upstream 브랜치명
     ```

   - 최적화

     ```bash
     $ git gc
     $ git gc --aggressive
     ```

     - 안전하고 확실한 최적화 방법

       ```bash
       $ git gc --aggressive --prune=now
       ```

       