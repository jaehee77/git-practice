<br />

### Git Config(설정파일)
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

<br />

### Git 초기화, 삭제하기 및 깃 별칭 설정하기
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


### Git add (staging area 로 올리기), status
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

<br />

### 파일 비교하기 diff
```bash
git diff
git diff --staged

# 파일비교를 에디터와 연결하기

```
<br />
<br />

### 버전 등록하기 commit
```bash
git commit -m "깃 버전 초기화 생성"

# 깃 히스토리 보기
git log

# git add 명령어도 같이 작성하기
# -am (all, message)
git commit -am "메시지 작성"
```

### 파일 변경시 주의해야햘 사항
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

<br />

### 깃 히스토리 알아보기(Log)
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


<br />

### 깃 로그 이쁘게 만들기(깃 로그 포맷팅)
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


<br />

### git 로그 사용자 커스텀
```bash
git log --graph --all --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short

# 위 포맷팅을 alias 로 저장하여 간편하게 사용하기
git config --global alias.hist "log --graph --all --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short"
```

<br />

### tag (태그의 필요성)
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

### 브랜치 사용법
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

# remote 혹은 upstream branch 으로 부터 파생된 새로운 local branch 생성하고 checkout하기
git checkout -b [remote_or_upstream branch_(ex: upstream/branch_name)] [new_local_branch_name] 
```

<br />

### Git 머지와 충돌해결 하기
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

# 머지할 때 충돌이 난다면 충돌해결 후에 git add . 를 하고 계속진행하라는 플래그를 작성
git add .
git merge --continue

# 머지 취소하기
git merge --abort

# 머지툴을 사용하는 경우 .orig 라는 백업파일이 생긴다면 백업파일을 생성하지 않도록 하기
git config --global merge.tool.keepBackup false

# 깃 청소하기
git clean -fd #(force 하게 directory 에 있는 것들을 clean)
```

<br />

### Rebase 란 무엇일까? 
리베이스를 이용하면 머지 충돌이 일어났을 때 three-way merge 를 하여  
머지 커밋이력을 남기지 않고 fast-forward merge 와 같은 방법을 사용할 수 있다.  
작업한 브랜치를 머지될 대상 브랜치의 최신 커밋 버전쪽으로 rebase 를 한다면  
fast-forward 가 가능해지게 된다.  
하지만 작업하는 브랜치가 다른 사람과 협업, 같이 작업하고 있다면 기존에 있던   
커밋 이력들이 달라지게 되기 때문에 주의해야 한다.  
특히나 원격 저장소에 작업중인 브랜치의 커밋 이력이 올라가 있다면(업로드)   
업로드된 히스토리는 건들면 안된다. 충돌이 발생하게 된다.  
즉, 서버에 업로드되지 않은 나의 로컬에 커밋에 한해서 rebase 를 하는 것은 편하게 할 수 있다.
```bash
# 머지할 곳의 브랜치의 최신 커밋 버전 포인터로 작업 브랜치를 rebase 한다.
git rebase master # feature/a 작업 브랜치를 머지할 곳의 마스터브랜치로 rebase 한다.

# rebase --onto
# 마스터에서 파생된 feature/a 브랜치에서 또 파생된 브랜치인 feature/a-ui 가 있을 경우
# feature/a-ui 를 마스터 브랜치로 머지하려고 하는 경우에 rebase --onto 를 사용할 수 있다.
git rebase --onto master feature/a feature/a-ui
# 역시, 서버에 올라가 있다면 주의해서 사용해야 한다.
```

<br />

### 원하는(특정한) 커밋 버전만 쏙 뽑아내기 cherry pick
```bash
# 뽑아올 대상 커밋 버전의 해쉬코드를 가져와서 머지될 대상 브랜치로 이동(여기선 마스터라고 가정)
git cherry-pick f2b9178 # 마스터 브랜치로 다른 브랜치의 커밋버전을 쏙 뽑아와서 머지함
```

<br />

### Stash 알아보기
working directory 에 변경이력이 있는 파일들이 있을 경우 커밋을 하지 않으면서  
다른 브랜치로 체크아웃하기 위해 사용한다. 
즉, 커밋하기에 준비되지 않은 파일들을 stash 스택에 저장해 두고 다른 브랜치로 이동하고  
다시 해당 브랜치로 돌아와서 stash 해 놓은 파일이력을 다시 꺼내온다.  
브랜치 전환을 위해서 잠시 저장해 놓을 수도 있고,  
여러개의 테스트 코드를 작성하는 경우에도 이용할 수 있다.
```bash
# git stash 만 작성하면  git stash push 와 동일하과 아무런 타이틀 없이 저장된다.
git stash

# 의미있는 이름으로 stash 에 저장하기
git stash push -m 'first 작업중인거 잠시 저장'

# staging area 에 파일을 add 해 놓은 상태이고 staging area 에 올라간 상태로  
# stash 에 저장해 놓고 싶다면 --keep-index 를 사용한다.
git stash push -m "stash try keep"

# untracked(추적하고 있지 않은) 파일도 stash 에 포함하고 싶다면
git stash -u # untracked 

# 전체적인 stash 목록 보기
git stash list 

# 특정한 stash 내용 보기
git stash show stash@{3} -p

# 해당 브랜치로 돌아온 후 stash 에 있는것을 가져오기
git stash apply stash@{2} # apply 만 작성하면 최신 stash 를 가져옴

# stash 를 적용하면서 목록에서 제거하고 싶다면 pop 을 이용하고
# 적용하면서 stash 목록을 유지하고 싶다면 apply 를 이용한다.
git stash pop 

# 필요없는 stash 목록 삭제하기
git stash drop stash@{3}

# 전체 stash 목록을 삭제하기
git stash clear

# stash 에 잠시 저장해 놓은 것을 새로운 브랜치를 생성하면서 stash 에 있는 것도 적용하기
# stash 목록에 하나만 있을 경우에 가능한 듯
git stash branch 브랜치명
```

<br />

## Git 취소하기, 수정하기, 리셋하기, 커밋 버전 삭제하기 등...
### 로컬에서 작업하는 파일이나 working directory 에서 작업하는 내용을 초기화하는 방법
> reset 은 내가 가고자하는 포인터를 가리킬 수 있다.
```bash
# working directory 안에 있는 파일 지워버리기
git restore 파일명
# working directory 안에 있는 파일 모두 버리기(삭제하기)
git resotre .

# staging area 에 파일이 있을 때 취소해서 working directory 로 가져가기
git restore --staged 파일명 # or .(dot)


# reset 은 내가 가고자하는 포인터를 가리킬 수 있다.
# staging 에 있는 모든 파일들이 다시 working directory 로 되돌려 놓을 수 있다.
git rest HEAD .

# 어떤 커밋으로부터 파일을 초기화할 것인지를 작성할 수 있다.
git restore --source=HEAD~2 파일명
```

<br />

### 커밋 메시지 및 파일내용을 업데이트하여 수정하기
> 로컬에서만 사용하길 권장(서버에 변경사항을 푸쉬하지 않았을 경우에 사용)
```bash
# 커밋 메시지 또는 커밋 메시지와 파일내용을 수정했을 경우
git commit --amend -m "modified message"

# 커밋한 파일의 내용만 수정했을 경우
git commit --amend
```

<br />

### 리셋 그리고 리셋
> 특정한 커밋 버전으로 모든 것을 초기화 시켜주는 명령어
```bash
git reset HEAD~2
# git reset --mixed  와 동일하다고 할 수 있다.
# 되돌리면 작업하여 커밋했던 내용들은 working directory 에 옮겨 놓게 된다.

git restore . 
# restore 를 한다고 해서 새로 추가된 파일이 삭제되지 않기 때문에
# 삭제를 해야 한다면 clean -fd 해주어야 한다.
git clean -fd

# HEAD 를 쓰지 않고 커밋아이디를 이용하기
git reset 3868bd

# --mixed 는 working directory 로 옮겨 놓지만
# --soft 는 staging area 로 옮겨 놓는다.
git reset --soft HEAD~1

# 그냥 다 working directory, staging area 도 남기지 말고 다 삭제하기
git reset --hard HEAD~2
```

<br />

### 실수로 모든 커밋을 날려서 reset 을 했다면.. 다시 복구하기
```bash
# 참조된 로그를 통해 hash code 를 확인하고 해당 해쉬코드를 이용하여 해당 커밋버전으로 돌아간다.
git reflog

git reset --hard 6f8c067
# 단, 커밋이 되어 있지 않은 경우에는 되돌릴 수 없다.
```

<br />

### 취소사항을 버전으로 남기기
리셋등을 이용하여 이전 버전으로 되돌리는 작업등의 취소하기를 하면  
취소한 내용이 커밋버전으로 남지가 않는다.  
하지만 이전 커밋으로 되돌리기 취소를 revert 를 이용한다면 취소하려는 커밋 내용들을 제거하면서  
커밋 내역까지 남기면서 버전 관리를 할 수 있다.
```bash
# 커밋 내용을 남기면서 해당 해쉬코드 커밋내용을 삭제
git revert fa7bbd6

# 커밋 내용을 남기지 않고 커밋 버전 삭제
# 이 경우에는 revert 하여 제거하려 했던 내용들은 staging area 에 옮겨놓게 된다.
git revert --no-commit 1d11be8
```

<br />

### 이전것들 중에서 커밋 메시지를 수정하기(혼자 작업한다면 강추)
> 이전것을 수정하면 수정하려는 커밋버전보다 나중(최신)의 커밋사항들도 업데이트된다는 점 유의!
```bash
# interactive
git rebase -i 9855fc
```


<br />

### Git Repository
```bash
# 원격 저장소가 있다면 어떤 저장소가 있는지 확인
git remote

# 원격 저장소에 대한 연결된 정보
git remote -v

# 다수의 리모트 저장소를 추가하기(여기서 업스트림은 저장소의 별칭을 의미)
git remote add upstream 깃허브링크(주소)


# 원격 저장소의 상세 정보보기
git remote show origin


git push
# 아이디와 패스워드 입력후 푸쉬 완료됨

# 원격 저장소의 커밋 버전이 더 앞서고 있고
# 로컬 저장소에도 변경 내역이 있다면 
# 즉, 원격과 로컬의 싱크가 맞지 않다면
# 로컬 저장소에 있는 것을 force 로 푸쉬하게 되면
# 원격 저장소에 변동 사항이 있더라도 내 로컬 내역을 강제로 푸쉬하면
# 원격 저장소에 있던 커밋 내역은 삭제되고 내 로컬 저장소에 있는 것이 올라가게 된다.
git push -f
```

<br />

### 이미 로컬에 만들어진 프로젝트를 원격저장소에 추가하기 및 기타
원격저장소에 저장소 생성후에 푸쉬
```bash
# orgin 이라는 별칭을 가진 저장소를 연결, 등록
git remote add origin https://github.com/jaehee77/git-practice.git
git push

# or 최초에 작성
git push --set-upstream origin master


```

<br />

### 저장소 다루기 (fetch & pull)
```bash
# remote 혹은 upstream branch 으로 부터 파생된 새로운 local branch 생성하고 checkout하기
git checkout -b [remote_or_upstream branch_(ex: upstream/branch_name)] [new_local_branch_name] 


# 원격저장소에 커밋 내역만 가져오기
# origin 별칭을 가진 저장소에 있는 master 브랜치 커밋 내역을 가져오기
git fetch origin master


git pull
# 동일한 파일에 로컬파일과 원격저장소에 있는 파일에 수정이 발생하여 충돌이 발생하면
# 충돌을 해결하고 나서 add 와 continue 를 하고 커밋 메시지 작성
git add .
git merge --continue

# 풀할 때 지저분한 커밋메시지를 남기지 않고 받아오기
# rebase 를 하면 서버에 있는 커밋을 가지고 와서 그 상태에서 로컬에 있는 커밋내용을 저장하면서
# 진행되기 때문에 로컬에서 충돌이 발생하게 되고 그 상태에서 동일하게 충돌을 해결하고
# rebase --continue 를 진행하면서 커밋메시지를 작성하도록 한다.
# 이렇게 진행하면 서버에 있는 커밋도 유지되고 내가 작성한 커밋도 유지된다.
git pull --rebase
# 충돌발생하면 충돌해결 후
git rebase --continue
git push
```


<br />

### 푸쉬를 간편하게 하기 SSH(Secure Share protocal)
서버에는 퍼블릭키를 개인 로컬에는 프라이빗키를 저장해 놓음으로써 푸쉬를 할때  
아이디와 비번을 입력하지 않게 사용할 수 있다.

<br />

### Upstream, Origin, Local repository
그 후 GitHub의 '[내 계정]/[프로젝트 명]' (Origin repository)을 내 개인 컴퓨터에 연결할 수 있다.   
연결을 통해 내 컴퓨터에 생성 및 저장된 프로젝트 폴더(.git)를 Local repository라 한다.   
만약 repository가 public이라면 $ git clone https://github.com/[내 계정]/[Project].git을 통해  
local repository를 만들 수 있지만, private repository라면 아래와 같이 token을 사용하여 clone할 수 있다

```bash
GitHup에서 [Settings]>[Developers settings]>[Personal access tokens]>[Generate new token]
Note 및 적절한 scopes (repo 등) 선택 후 [Generate token]
생성된 [Token] 복사해 둠.

# 사용자 설정 (1)
$ git config --global user.name "[이름]"
$ git config --global user.email [이메일]

# 사용자 설정 확인
$ git config --list

# Clone private repository
$ git clone https://[이름]:[Token]@github.com/[내 계정]/[Project].git
```

마지막으로 개인 컴퓨터에 Upstream repository를 등록한다.

```bash
$ cd [Project]
$ git remote add upstream https://github.com/[관리자 게정]/[Project].git

# 다음의 명령어로 확인 가능
$ git remote
> origin
> upstream
```

이렇게 하면 3종류의 repository 및 각각의 master branch (총 3종류)가 존재하게 된다.  
새로운 작업을 하기 전에는 모든 master branch의 내용이 같은지 확인을 하고, 다르면 맞춰줄 필요가 있다. 

1. local 에서 branch에서 Upstream Repository의 branch를 pull (git pull upstream 내작업브랜치)한다
2. Local branch에서 나의 원격 저장소의 브랜치로 push(git push origin 내작업브랜치)한다.

Upstream master에 내가 개발한 내용을 푸쉬를 해야한다면 먼저 Local work(로컬 저장소)의 내용을
Origin work(내 원격저장소)에 push 한다.  

```bash
 $ git push -u origin work
 ```
그 후, 깃헙이나 깃랩 사이트에서 원격저장소의 작업 branch를  
Upstream Repository의 master branch로 pull request한다.   
검토 결과 이상이 없으면 담당자 또는 누군가에 의해서 Merge pull request 가 진행된다.


<br />

### Master 브랜치 내용을 작업 브랜치로 업데이트
만약 개발기간이 길어져서 Upstream 내용이 로컬 작업 브랜치에 필요하다면  내용을 풀 받아서 진행해야 한다.  
먼저 로컬 작업브랜치에서 업스트림 브랜치를 pull (git pull upstream 내작업브랜치)하고,    
로컬 작업 브랜치에서 내 원격저장소의 브랜치로 push (git push origin 내작업브랜치)한다.
```bash
$ git pull upstream master
$ git add .
$ git commit -m "Sync with upstream master"
$ git push origin work
```

<br />

### 자주쓰는 명령어를 깃 단축 명령어로 등록하기
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.up "!git fetch origin master && git rebase origin/master"
git config --global alias.ca "!git add -A && git commit -m"
git config --global alias.apply "stash apply"
git config --global alias.pop "stash pop"
```