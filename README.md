## Git Config(설정파일)
```bash
# 설정파일 목록 보기
git config --list

# 설정파일을 VS Code 로 여는 것을 설정하는 방법
git config --global core.editor "code"

# 설정파일이 에디터로 열리고 설정파일을 닫을때 까지 기다리게 하는 방법
git config --global core.editor "code --wait"

# 에디터 설정을 하지 않았다면 기본 터미널에서 설정파일을 편집모드로 열고
# 에디터를 설정했다면 설정한 에디터에서 설정파일을 오픈함
git config --global -e

# 설정파일에 이름과 이메일 설정
git config --global user.name "jaiyah"
git config --global user.email "jaiyah@naver.com"
# 설정해 놓은 이름과 이메일 확인하기
git config user.name
git config user.email

# new line(개행) 설정하기 ::: MAC(input), Window(true)
# 운영체제마다 새로운 줄바꿈을 할때마다 삽입되는 문자열이 달라지는데 
# 윈도우는 \r\n (carriage-return, linefeed) 가 동시에 삽입되며
# Mac 은 \n 하나만 들어가게 된다.
# 깃 저장소를 다양한 운영체제에서 쓰는 경우에 본인이 수정하지 않았음에도 불구하고
# 줄바꿈 문자열이 달라져서 깃 히스토리를 보는데 문제가 발생할 여지가 있다
# 윈도우에서 저장할 때는 캐리지리턴을 삭제하게 되고 다시 깃에서 가져올 때는
# 자동으로 캐리지리턴을 붙여준다.
# 맥에서 input 으로 설정하게 되면 깃에서 받아올 때는 별다른 수정이 일어나지 않지만
# 저장할 때는 캐리지리턴을 삭제처리한다.
# 맥에서 캐리지리턴이 붙지 않음에도 불구하고 이렇게 설정하는 것은
# 맥에서 이메일을 받아온 텍스트를 복사해서 붙여넣을 때 
# 캐리지리턴이 실수로 들어갈 수 있기 때문이다.
git config --global core.autocrlf input
git config --global core.autocrlf true
```

## Git 초기화, 삭제하기 및 깃 별칭 설정하기
```bash
# 깃 초기화
git init

# Tip: 숨김파일 목록까지 보는 명령어
ls -al

# 깃 파일열기(윈도우 start, 맥 open)
start .git
open .git

# 깃 삭제하기
rm -rf .git

# 깃 단축어 설정하기
# git status 를 타이핑하지 않더라도 git st 만 치더라도 상태를 확인 가능
git config --global alias.st status
```
<br />

## Git add (staging area 로 올리기), status
```bash
# staging area 에 추가하기(깃 버전을 생성할 준비가 된 단계)
git add .
git add *.txt
git add a.txt b.txt

# 깃 버전 관리되기 전 상태로 되돌리기
# 즉, working directory 의 untracked 상태로 되돌리기
git rm --cached a.txt
git rm --cached *

# .(dot) vs *(에스타리스크) 의 미묘한 차이 
# dot 쓰는 것이 더 편함, 버전관리가 용이

# 깃 상태 도움말 확인하기
git status -h

# 깃 상태 간단히 보기
git status -s
```

## 파일 비교하기 diff
```bash
git diff
git diff --staged

# 파일비교를 에디터와 연결하기

```

## 버전 등록하기 commit
```bash
git commit 

# 깃 히스토리 보기
git log
```
