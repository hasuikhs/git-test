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
$ git status

// 상태를 찍으면 충돌난 파일이 보여진다
<<<<<<< HEAD
// 현재 체크 아웃된 내용
=========
// 병합하려는 대상인 내용
>>>>>>> master
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


## 3. git 취소하기

### 3.1 git add 취소하기

```bash
$ git reset Head [file]	# 파일명

$ git reset Head		# 파일명이 없으면 add 전체 취소
```

### 3.2 git commit 취소하기

- commit 목록 확인

  ```bash
  $ git log
  ```

- commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉토리에 보존

  ```bash
  $ git reset --soft HEAD^
  ```

- commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉토리에 보존

  ```bash
  $ git reset --mixed HEAD^	# 기본 옵션
  
  $ git reset HEAD^			# 기본 옵션
  
  $ git reset HEAD~2			# 마지막 2개의 commit을 취소
  ```

- commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉토리에서 삭제

  ```bash
  $ git reset --hard HEAD^
  ```

- commt message 변경하기

  ```bash
  $ git commit --amend
  ```