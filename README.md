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
git commit -m "깃 버전 초기화 생성"

# 깃 히스토리 보기
git log

# git add 명령어도 같이 작성하기
# -am (all, message)
git commit -am "메시지 작성"
```

## 파일 변경시 주의해야햘 사항
```bash
# 파일을 rm 만 작성하여 삭제하는 경우에는 staging area 에 추가되지 않기 때문에
# 즉, 삭제된 파일이 버전 관리가 되지 않은 상태라서 git add 를 추가하고 
# commit 을 해주어야하는 번거로움이 있지만
# git rm a.txt 를 이용하면 바로 버전관리가 되어 자동으로 staging area 에 추가된다.

# rm a.txt (X) 보단...
git rm a.txt
git status

# 마찬가지로 파일이름 변경시에도 
# mv c.txt d.txt
# git status 에는 포함되지 않지만
# git rm 을 이용하면 status 에 자동으로 포함된다.
git mv b.txt b-1.txt
```

## 깃 히스토리 알아보기(Log)
```bash
# 상단에 있는 목록이 최근 로그이며 아래 방향키로 이전 목록들을 확인할 수 있음
git log

# 변경된 내역들 상세보기
git log --patch # -p(단축어)

# 내역 간단히 보기
git log --oneline

# 오래된 내역부터 보기
git log --oneline --reverse
```


## 깃 로그 이쁘게 만들기(깃 로그 포맷팅)
```bash
git log --pretty=oneline


# hash 코드와 author name 만 보고 싶다면..
git log --pretty=format:"%h %an"

# %ar 날짜, %s 타이틀
git log --pretty=format:"%h %an %ar %s"

# 로그와 모든 브랜치 내역까지 함께 보기
git log --oneline --graph --all

# 최근 로그 내역 갯수지정하여 보기
git log -3 
git log --oneline -3

# 작성자만 보기
git log --author="jaiyah"

# 지정된 날짜 이전꺼 보기
git log --before="2022-09-20"

# 커밋 타이틀 중에서 찾고자하는 텍스트로 찾기
git log --grep="project"

# 소스 콘텐츠 안에서 문자열을 검색하기
git log -S "find text" # -p(--patch) 좀더 자세한 내역

# 파일별로 로그 내역보기 (파일에 해당하는 커밋이력을 볼 수 있음)
git log a.txt
git log a.txt -p
git log a.txt -s # -s(--short) 간단히 보기

# 해쉬코드로 로그 보기
git show 0ad2dbb
git show 0ad2dbb:file.txt # 파일의 내용 로그만 보기
```

## git 로그 사용자 커스텀
```bash
git log --graph --all --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short

# 위 포맷팅을 alias 로 저장하여 간편하게 사용하기
git config --global alias.hist "log --graph --all --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short"
```

<br />

## tag (태그의 필요성)
특정한 커밋 버전을 북마크해두고 싶을 때 사용한다.  
특정한 커밋을 태그해 놓음으로써 사용자가 원하는 부분으로 빠르게 전환할 수 있으며  
일반적으로 제품을 릴리즈할 때 그 버전을 태그해 놓는다.  
이처럼 태그는 길다란 버전 히스토리에 특정한 부분을 태그해 둠으로써   
언제 릴리즈버전이 되었는지 태그별로 관리를 하기 쉽고 전환이 빠른 장점이 있다.

```bash
git tag v1.0.0

# 특정한 커밋 버전에 태그(북마크)해 두기
git tag v1.0.1 해쉬코드 

# 특정한 커밋 버전에 상세한 내용 기록하기 (anotate)
git tag v2.0.0 32808d -a -m "Release Note.."
git tag v2.0.0 32808d -am "Release Note.."

# 태그의 주석내용까지 보기
git show v2.0.0

# 북마크된 모든 태그 보기
git tag

# 태그 목록중에 어떤 특정한 문자열이 있는 것만 보기
git tag -l "v1.0.*" # *(와일드카드) 사용
git tag -l "v2.*"

# 실수로 만든 태그 삭제하기
git tag -d v1.0.0

# 태그된 커밋버전으로 이동하기
git checkout v2.0.0

# 새로운 브랜치를 만들면서 태그도 함께 하기
git checkout -b testing v2.1.0

# 리모트저장소에도 태그를 업로드하기
git push origin v2.0.0

# 모든 태그들을 업로드하기
git push origin --tags

# 리모트 저장소에 있는 특정한 태그삭제하기
git push origin --delete v2.0.0
```

<br />

## 브랜치 사용법
```bash
# 로컬 브랜치만 확인하기
git branch

# 리모트저장소를 포함한 모든 브랜치 보기
git branch --all

# 브랜치 생성하기
git branch 브랜치명

# 만든 브랜치로 이동하기
git switch 브랜치명 

# 브랜치를 만들자마자 해당 브랜치로 이동하는 방법 2가지
# checkout 은 브랜치 이동이나 해쉬코드를 이용하여 해당 버전으로 이동이 가능
git checkout -b 브랜치명
git switch -C 브랜치명 # -C(create)

# 브랜치별로 최신 커밋들 확인해보기
git branch -v

# 현재 사용자가 있는 브랜치에서 병합이 된 브랜치들 보기
git branch --merged

# 현재있는 곳 브랜치에서 머지가 되지 않은 브랜치들 보기
git branch --no-merged

# 머지(병합)하기
# 머지될 타켓 브랜치로 이동한 후 머지할 대상 브랜치를 작성
git merge feature/a # 이동한 타켓 브랜치가 master 라면 마스터브랜치에 feature/a 를 병합하는 것임

# 로컬 브랜치 삭제하기
git branch -d 브랜치명

# 원격저장소에 있는 브랜치도 삭제하기
git push origin --delete 브랜치명
git push origin -d 브랜치명

# 로컬 브랜치 이름 변경하기
git branch --move 대상브랜치명 변경할이름브랜치명

# 이름이 변경된 브랜치도 원격저장소에 업데이트하기
git push --set-upstream origin 변경된이름브랜치명

# 리모트 저장소 살펴보기
git remote show origin
git remote show upstream

# 브랜치와 브랜치사이의 커밋 정보들만 보기
git log master..feature/a

# remote 혹은 upstream branch 가져와 새로운 local branch 생성하고 checkout하기
git checkout -b [new_local_branch_name] [remote_or_upstream branch_(ex: upstream/branch_name)]
```


## Git 머지하기
예를 들어, master 브랜치에서 브랜치를 생성해서 작업한 후 작업한 브랜치를 마스터 브랜치로  
머지하려고 할 때 머지하는 시점에 마스터 브랜치에 더이상의 커밋이력이 없고 작업브랜치를 머지하려고 하면   fast-forward-merged 를 하게 되어 머지커밋 이력이 남지 않고 머지하게 된다.
하지만 fast-forward-merged 를 하고 싶지 않다면 --no--ff(no-fast-forward) 를 하면  
머지 커밋이력을 남기고 머지할 수 있다.
```bash
# 머지목적지 대상브랜치로 이동한 후 작업한 브랜치를 머지한다.
# 예를 들어, master 브랜치로 머지를 해야한다면 master 로 이동한 후 작업한 브랜치를 머지한다.
git merge feature/b

# 변경이력남겨서 머지하기 (fast-forward-merged 하지 않고)
git merge --no-ff feature/b
```