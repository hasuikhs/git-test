## GIT

1. #### 사전 준비

   - VS Code 설치(https://code.visualstudio.com/download)
   - 자신의 OS와 맞는 버전 설치
   - python 설치
   - flask 설치

2. #### Git Bash

   - 작업하고자 하는 폴더에서 우클릭 후 git bash 실행

   - 최초 실행시 진행

     - git commit에 사용될 username 설정
   
       ```bash
       $ git config --global user.name "user_name"
       ```
   
     - git commit에 사용될 email
   
       ```bash
       $ git config --global user.email "your_email@example.com"
       ```
       
     
- 해당 폴더를 git에 올릴 로컬 저장소로 설정
  
  - 로컬 저장소로 사용할 위치로 이동
    
       ```bash
       $ cd 경로
       ```
       
  - 해당 폴더에서 vs code를 바로 실행하는 명령어
    
     ```bash
     $ code .
     ```
     
  - git 시작
    
    ```bash
    $ git init
    ```
    
   - git 명령어
  
     - 현재 상태를 보여준다.
  
       ```bash
       $ git status
       ```
  
     - 현재까지의 log 보기
  
       ```bash
       $ git log
       ```
  
   - git 로컬 저장소(사용자 컴퓨터)에 저장
  
      - 파일 별로 저장하는 방법
      
        ```bash
        $ git add (파일명)
        ```
        
     - 해당 경로의 폴더를 통째로 저장하는 방법
     
          ```bash
          $ git add .
          ```
     
     - add 후 commit
     
          ```bash
          $ git commit -m "commit comment"
          ```
     
          - commit 명은 날짜|내용으로 하는 것을 추천한다. 예) 191231|Add comment
          
          - 이전 commit comment를 수정하려면
          
            ```bash
            $ git commit --amend
            ```
     
  - github의 원격 저장소에 저장
  
       - 원격 저장소 설정
  
            ```bash
            $ git remote add origin http://github 주소
            ```
  
       - 저장소로 넣기
  
            - 최초 설정시
  
                 ```bash
                 $ git push -u origin master
                 ```
  
            - 최초 설정 후
  
                 ```bash
                 $ git push 
                 ```
       
   - github 저장소에서 내려받기
  
     - 최초 해당 github 원격 저장소의 내용 받기
     
       ```bash
       $ git clone http://내려받을 github 주소
       ```
     
     - 최초로 받은 후의 명령어
     
       ```bash
       $git pull
       ```
  
- **이 과정을 반복 clone - add - commit - push - pull - add - ...**

