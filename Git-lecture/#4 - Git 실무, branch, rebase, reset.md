# Git 실무 - with VSCode

## Git Branch 
	1. Master 브랜치는 항상 Deploy할 수 있는 상태로 두자!
	2. 작업할 때는 항상 Topic 브랜치를 만들어서 하자!
	3. 브랜치 이름은 누가봐도 알 수 있도록 자세히 짓자!
	4. 정기적으로 자주 push하자!
	5. Merge가 끝나면 해당 Topic 브랜치는 바로 삭제하자
	(remote branch의 경우 push하고 삭제)
	
	
### 실무에서 자주 쓰이는 명령어
```
$> git branch [-a | -r]
$> git branch <new-branch> [<from-br>]
$> git checkout <branch-name>
$> git checkout -b <new-br> <from-br>
$> git checkout -
$> git checkout master
$> git checkout -p <branch> <file>

# --no-ff : fast-forward를 하지 않겠다. 항상 --no--ff로 하는게 좋다.
$> git merge --no-ff <branch>
$> git log --graph
$> git branch [-d|-D] <branch-name>
$> git push -d origin <br>

# 커밋 메시지 변경 명령어
$> git commit --amend     ⇐ REWORD

# 의미가 없는 연속된 커밋 메시지는 rebase로 합쳐준다. 
$> git rebase -i HEAD~2    # --abort
$> git reflog
$> git reset --hard <revision-hash-id>
$> git reset --hard <tag>
$> git push -u origin master  ⇐ Upstream
$> git revert <revision-hash-id>
$> git revert <revision-hash-id> -- <path>
```


# Git Rebase & Reset/Revert/Tag

### rebase
1. 하나의 Commit은 하나의 의미만 갖자!
2. rebase  ($> rm -fr ".git/rebase-merge")

rebase 옵션
-  drop: 해당 소스(commit) 삭제!  (cf. reword)
-  fixup: 바로 앞(previous)으로 합치기, 소스는 살아있음
-  squash: 바로 앞(previous)을 최신으로 합치고,  commit 메시지 변경가능

3. reset은 push 전, revert는 push 후!

```
# 의미가 없는 연속된 커밋 메시지는 rebase로 합쳐준다. 
$> git rebase -i HEAD~2    # --abort
```

### reset
Working 디렉토리에서 add하면 stage영역으로 이동하고 commit하면 .git 폴더로 이동합니다.
```
# Stage 영역에 파일을 Working 디렉토리로 되돌리고 싶다면
$ git reset HEAD

# .git영역에서 커밋된 파일을 stage영역으로 되돌리고 싶다면 
$ git reset --soft HEAD~

명령어를 사용합니다.

```
### Tag
태그는 릴리즈되는 단위, 즉, 배포되는 단위를 설정할 때 사용합니다.
```
# 태그 기록
$> git tag

# 태그 생성
$> git tag v0.0.1

#태그 서버에 PUSH
$> git push origin [--tags | v0.0.1]

#태그 삭제
$> git tag -d <tag>

#서버에 태그 삭제
$> git push origin -d <tag>
```



