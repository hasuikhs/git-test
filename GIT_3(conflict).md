# GIT_3(conflict)

- 여러명이 같은 branch에서 fork하여 각각의 branch로 작업 후 작업 후 push, merge에서 conflict error 발생

## 0. 시나리오

### 0.1 branch

#### 0.1.1 stage branch

- 원본 소스를 가진 branch

#### 0.1.2 test1 branch

- stage branch에서 파생된 branch

  ```bash
  $ git clone [git repository] -b stage
  ```

- test1 branch 생성

  ```bash
  (stage)$ git branch test1
  
  (stage)$ git checkout test1
  ```

- 작업 후 push

  ```bash
  (test1)$ git add .
  
  (test1)$ git commit
  
  (test1)$ git push origin test1
  ```
  
- stage에 merge

  ```bash
  (test1)$ git fetch origin
  
  (test1)$ git checkout stage
  
  (stage)$ git fetch
  
  (stage)$ git merge test1
  
  (stage)$ git add .
  
  (stage)$ git commit
  
  (stage)$ git push
  
  (stage)$ git checkout test1
  ```

#### 0.1.3 test2 branch

- stage branch에서 파생된 branch

  ```bash
  $ git clone [git repository] -b stage
  ```

- test1 branch 생성

  ```bash
  (stage)$ git branch test2
  
  (stage)$ git checkout test2
  ```

- 작업 후 push

  ```bash
  (test2)$ git add .
  
  (test2)$ git commit
  
  (test2)$ git push origin test2
  ```

- stage에 merge

  ```bash
  (test2)$ git fetch origin
  
  (test2)$ git checkout stage
  
  (stage)$ git fetch
  
  (stage)$ git merge test2
  
  # modify conflict error 
  
  (stage)$ git add .
  
  (stage)$ git commit
  
  (stage)$ git push
  
  (stage)$ git checkout test2
  ```

## 1. 과정

- test1 branch는 conflict가 나지 않아 계속 자신의 branch를 이어가 자신의 위치를 계속 가져감

- test2 

  - 방법1 : test2 branch는 conflict가 났으므로 자신의 로컬 소스를 버리고 stage에서 다시 clone하고 branch를 overwrite하여 사용
  
  ```bash
  $ cd ..
  
  $ rm [/dir]	# 이전 소스 삭제
  
  $ git clone [git repository] -b stage
  
  (stage)$ cd [/dir] # 새로 받은소스로 이동
  
  (stage)$ git branch test2
  
  (stage)$ git checkout test2
  ```
  
  - 방법2 : stage로 scope를 옮긴 상태에서 자신의 브랜치를 버리고 새로 이름이 같은 브랜치를 생성하여 사용
  
  ```bash
  (stage)$ git branch -D test2
    
  (stage)$ git branch test2
    
  (stage)$ git checkout test2
  ```

  