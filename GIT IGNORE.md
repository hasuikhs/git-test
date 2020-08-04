# Git IGNORE

> local에서 remote로 올리고 싶지 않거나 올려서는 안되는 파일, 폴더를 제외하는 파일

## 1. `.gitignore`만들기

- 항상 최상위 Directory에 존재해야 함
- `.gitignore`로 생성

- [gitignore.io](gitignore.io) 에서 IDE나 언어에 따라서 쉽게 생성하여 붙여넣기 해도 좋음
- 그 외 폴더나 파일들을 제외시키고 싶다면 직접 작성



## 2. 적용하기

### 2.1 git에 올리기 전 생성한 경우

- git에 올리기 전 생성한 경우는 특별히 문제가 되지 않음

### 2.2 git에 이미 올라가 있는 remote가 있는 경우

- `.gitignore`를 뒤늦게 추가해줬거나 잘못된 `.gitignore`를 올리고 나중에 발견한 경우

```bash
$ git rm -r --cached .

$ git add .

$ git commit -m "comment"
```

### 2.3 이미 추적 중인 파일 몇 개만 무시할 경우

- `.gitignore`를 사용 중 무시할 파일을 더 추가했을 경우

```bash
$ git rm -r --cached 파일1 파일2 ...

$ git add .

$ git commit -m "comment"
```

### 2.4 `.gitignore`에 있는 파일을 다시 추적하고 싶은 경우

- `-f ` 옵션을 사용하여 강제로 add

```bash
$ git add -f 파일명
```

