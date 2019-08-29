## GIT_2

1. #### Branch

   - 독립적으로 어떤 작업을 진행하기 위한 개념
   - 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않아
   - 여러 작업을 동시에 진행이 가능

   1. ##### branch 만들기

      ```
      git branch <branch name>
      ```

   2. ##### branch 전환하기

      ```
      git checkout <branch name>
      
      // 브랜치 만들기와 체크아웃을 한번에 하는 방법
      git checkout -b <branch name>
      ```

   3. ##### branch 병합하기

      ```
      // 다른 branch로 checkout 된 상태에서 
      // 즉, 다른 branch에서 add 와 commit을 한 후에
      // 다시 master branch로 checkout
      git merge <branch name>
      
      // 충돌 발생시 해당 파일의 코드로 이동하여 해결 후 add와 commit
      ```

   4. ##### branch 삭제하기

      ```
      // 다른 branch의 내용이 모두 master로 통합되었기에 필요하지가 않다
      git branch -d <branch name>
      ```

      