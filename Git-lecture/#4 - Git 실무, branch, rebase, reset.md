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
# 브랜치 확인
$ git branch [-a | -r]

# 브랜치 생성
$ git branch <new-branch> [<from-br>]

# 브랜치로 이동
$ git checkout <branch-name>

# 브랜치 생성과 체크아웃(이동)을 한번에 한다.
$ git checkout -b <new-br> <from-br>

#master로 브랜치 이동
$ git checkout -
$ git checkout master

# 현재 작업폴더에 브랜치의 file을 패치함
$ git checkout -p <branch> <file>

# 브랜치를 병합한다.
# --no-ff : fast-forward를 하지 않겠다. 항상 --no--ff로 하는게 좋다.
$ git merge --no-ff <branch>

# log를 그래프로 보여준다.
$ git log --graph

#브랜치를 삭제합니다., -D 옵션은 강제로 삭제합니다.
$ git branch [-d|-D] <branch-name>

#서버에 브랜치를 원격 삭제합니다.
$ git push -d origin <br>

# 커밋 메시지 변경 명령어
$ git commit --amend     ⇐ REWORD

# 의미가 없는 연속된 커밋 메시지는 rebase로 합쳐준다. 
#HEAD에서 2번째까지 
$ git rebase -i HEAD~2    # --abort

# git log 명렁어를 사용하면 현재 브랜치의 로그만 확인할 수 있다. 
#반면 git reflog라는 명령어를 사용하면 현재 저장소에서 수행된 모든 commit로그를 확인할 수 있다.
$ git reflog

$ git push -u origin master  ⇐ Upstream

# 의미가 없는 연속된 커밋 메시지는 rebase로 합쳐준다. 
$ git rebase -i HEAD~2    # --abort

# 특정 커밋으로 되돌아갈 수 있는데 되돌린 버전 이후의 버전들은 히스토리에서 삭제됩니다.
$ git reset --hard <revision-hash-id>
$ git reset --hard <tag>

# reset과 비슷하지만 되돌린 버전 이후의 버전들의 히스토리가 삭제되지 않고 새로운 log가 추가됩니다.
$ git revert <revision-hash-id>
$ git revert <revision-hash-id> -- <path>

# 서버 브랜치와 로컬 브랜치 업데이트(동기화), 로컬브랜치는 따로 삭제
$ git remote update --prune

```

## Git Rebase & Reset/Revert/Tag
### rebase
1. 하나의 Commit은 하나의 의미만 갖자!
2. rebase  ($ rm -fr ".git/rebase-merge")
rebase 옵션
-  drop: 해당 소스(commit) 삭제!  (cf. reword)
-  fixup: 바로 앞(previous)으로 합치기, 소스는 살아있음
-  squash: 바로 앞(previous)을 최신으로 합치고,  commit 메시지 변경가능
3. reset은 push 전, revert는 push 후!
```
# 의미가 없는 연속된 커밋 메시지는 rebase로 합쳐준다. 
$ git rebase -i HEAD~2    # --abort

# 특정 커밋으로 되돌아갈 수 있는데 되돌린 버전 이후의 버전들은 히스토리에서 삭제됩니다.
$ git reset --hard <revision-hash-id>
$ git reset --hard <tag>

# reset과 비슷하지만 되돌린 버전 이후의 버전들의 히스토리가 삭제되지 않고 새로운 log가 추가됩니다.
$ git revert <revision-hash-id>
$ git revert <revision-hash-id> -- <path>

```
### reset
Working 디렉토리에서 add하면 stage영역으로 이동하고 commit하면 .git 폴더로 이동합니다.
```
# Stage 영역에 파일을 Working 디렉토리로 되돌리고 싶다면
$ git reset HEAD
# .git영역에서 커밋된 파일을 stage영역으로 되돌리고 싶다면 
$ git reset --soft HEAD~1
명령어를 사용합니다.
```
### Tag
태그는 릴리즈되는 단위, 즉, 배포되는 단위를 설정할 때 사용합니다.
```
# 태그 기록
$ git tag
# 태그 생성
$ git tag v0.0.1
#태그 서버에 PUSH
$ git push origin [--tags | v0.0.1]
#태그 삭제
$ git tag -d <tag>
#서버에 태그 삭제
$ git push origin -d <tag>
```
## Fork & Pull Request (Social Coding)
​
-   오픈소스를 fork하면 내 레파지토리에 복제본이 생깁니다.
-   복제본으로 내 로컬 저장소에 clone해서 작업 한 것을 서버에 push하고,
-   여기서 뭔가 버그를 수정했다면 수정한 것을 원본에 반영해달라고 요청하는 것이 pull request 입니다.Fork & Pull Request on Git Service
​
```
# Fork & Pull Request on Git Service
1. Fork Repository to my GitHub //내 깃허브로 복제 Fork
2. Clone to Local // 로컬에 복제
3. Make Topic Branch //브랜치 생성
    $ git checkout -b <topic-branch> master
4. Edit Code
5. Diff, Add & Commit to Topic Branch
6. Push to Remote Topic Branch
    $ git push origin <topic-branch>
7. Change branch to Topic on GitHub
8. Compare & Pull Request
```

### Forked Repository Management (upstream)

-   원본 오픈소스를 수정했을 때 내 로컬에 저장된 clone에 수정된 부분이 들어와야합니다.
-   그래서 upstream을 뚫어서 fetch를 해줄겁니다.

```
# Forked Repository Management (upstream)
1. Fork & Clone (already)

# 원본 레파지토리 url로 upstream 연결하기
2. Add Upstream (Original Repository)
    $ git remote add upstream <url>

# upstream에 패치하고    
3. Fetch upstream/master Branch
    $ git fetch upstream

# master로 upstream 병합하기
4. Merge upstream/master → master
    $ git checkout master
    $ git merge upstream/master

5. Eidt & Add & Commit to Topic Branch
6. Push to Remote Branch
7. Send Pull Request & Conversation
```

## Pull Request (Code Review)

```
# Collaborator                             # Author(Leader) 
1. Clone to Local
2. Make Topic Branch
3. Edit Code
4. Add & Commit to Topic Branch
5. Push to Remote Branch
6. Send Pull Request to review         ⇒           Code Reviewing
                                        ⇐      Approve & Merge to master

7. Pull master & Remove Branch // 서버 브랜치와 로컬 브랜치 동기화
    $ git remote update origin --prune
```