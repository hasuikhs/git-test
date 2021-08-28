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
   
# 브랜치 만들기와 체크아웃을 한번에 하는 방법
$ git checkout -b <branch name>
   ```

### 1.3 branch 병합하기

   ```bash
# 다른 branch로 checkout 된 상태에서 
# 즉, 다른 branch에서 add 와 commit을 한 후에
# 다시 master branch로 checkout
$ git merge <branch name>
   
# 충돌 발생시 해당 파일의 코드로 이동하여 해결 후 add와 commit
$ git status

# 상태를 찍으면 충돌난 파일이 보여진다
<<<<<<< HEAD
# 현재 체크 아웃된 내용
=========
# 병합하려는 대상인 내용
>>>>>>> master
   ```

### 1.4 branch 삭제하기

   ```bash
# 다른 branch의 내용이 모두 master로 통합되었기에 필요하지가 않다
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


## 3. git 변경과 취소

### 3.1 git add 취소하기

```bash
$ git reset Head [file]	# 파일명

$ git reset Head		# 파일명이 없으면 add 전체 취소
```

### 3.2 git commit 수정하기

- --amend 옵션으로 마지막 커밋 수정

```bash
$ git commit --amend -m "new commit comment"
```

### 3.3 git commit 취소하기

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

### 3.4 git commit 통합하기

- 과거의 commit 통합

  ```bash
  $ git rebase -i HEAD~~
  ```

  - 애디터가 열리면 `HEAD` 에서 `HEAD~~`까지의 commit 표시

  - 통합될 commit의 `pick`을 `s`로 바꾸고 저장

    - rebase 실행 후 command option

      ```bash
      #  p, pick = use commit
      #  r, reword = use commit, but edit the commit message
      #  e, edit = use commit, but stop for amending
      #  s, squash = use commit, but meld into previous commit
      #  f, fixup = like "squash", but discard this commit's log message
      #  x, exec = run command (the rest of the line) using shell
      ```

  - `git log` 로 이력 확인


## 4. 임시 저장

- 현재 작업 일시 저장 save는 생략 가능

  ```bash
  $ git stash save
  ```

- 일시 저장 목록 확인

  ```bash
  $ git stash list
  ```

- 일시 저장 작업 불러오기

  - stash 리스트에서 삭제하면서 가져오기

    ```bash
    $ git stash pop
    ```

  - statsh 리스트에서 삭제하지 않고 가져오기

    ```bash
    $ git stash apply
    ```

- 일시 저장 작업해둔 작업 삭제

  ```bash
  $ git stash drop
  ```

- 일시 저장 작업 모두 삭제

  ```bash
  git stash clear
  ```
