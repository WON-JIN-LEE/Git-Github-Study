# 3 - Git Branch / merge

## 깃 브랜치는 무엇인가?

모든 버전 관리 시스템은 브랜치를 지원한다. 개발을 하다 보면 코드를 여러 개로 복사해야 하는 일이 자주 생긴다. 코드를 통째로 복사하고 나서 원래 코드와는 상관없이 독립적으로 개발을 진행할 수 있는데, 이렇게 독립적으로 개발하는 것이 브랜치다.

즉, 나무의 몸통은 master이고 나무 가지를 브랜치라고 할 수 있습니다.

주의할 점은 브랜치를 생성 및 변경 전에 commit 하는 것을 잊으면 안 됩니다.  
현재 위치에서 커밋을 하고 브랜치를 이동하거나 생성해야 오류가 발생하지 않습니다.

## 브랜치(Branch) 명령어

- 브랜치 생성

```
$ git branch <branch-name> # branch 만들기
$ git branch   # branch 전체 보기
```

- 브랜치 이동

```
$ git checkout <branch-name>   # 전환

소스 수정 & add & commit

$ git push origin <branch-name> # 서버에 브랜치 push
```

- local과 server 브랜치 삭제 방법

```
# branch 삭제
# local
$ git branch -d <branch-name>

# local
$ git branch

# remote
$ git push --delete origin <branch-name>
```

- branch를 확인하는 방법

```
# 로컬(PC) 브랜치 보기
$ git branch

# 서버(GitHub) 브랜치 보기
$ git branch -r

# 양쪽 모두 보기
$ git branch -a
```

- 현재 브랜치와 브랜치 간의 차이점을 보여준다.

```
$ git diff <branch-name>
$ git diff <branch-name> <file-name>
```

- git checkout는 브랜치 이동이지만 -p옵션을 붙이면 브랜치를 작업 파일에 패치를 한다.

```
# 즉, 패치이므로 현재 브랜치의 수정 내용과는 관계 없이 해당 파일의 내용으로 변경된다.
$ git checkout -p <branch-name> <file-name>
$ git checkout -p <branch-name>
```

- 브랜치의 특정 파일만 master로 커밋해서 올리기

```
$ git checkout master
$ git checkout -p <branch-name> <file-name>
$ git add <file-name>
$ git commit -am "message"
$ git push origin master
```

- 서버의 특정 브랜치 가져오기, 작업한 브랜치 파일 push/pull 명령어

```
#서버의 특정 브랜치 가져오기
$ git checkout -t origin/<branch-name>

# 특정 브랜치 pull 하기
$ git pull origin <branch-name>

# 특정 브랜치 push 하기
$ git push origin <branch-name>
```

---

## Git merge (브랜치 병합)

Git을 버전 관리시스템으로 두고 같이 협업하는 과정에서 브랜치를 만들어서 각자 개발을 했다면, 그 브랜치들을 메인 master 브랜치에 합치는 것(병합)을 merge라 한다.

예를 들면 브랜치 a와 b가 있다고 가정했을 때 a로 b를 merge 하고 싶다면 내 브랜치 위치를 수신받을 브랜치로 이동해야 한다. a 브랜치로 이동한 뒤 merge를 수행해야 합니다.

즉, 작업할 폴더에서 merge를 수행해야 합니다.

### master로 merge 하기

```
$ git checkout master    #master로 변경
$ git merge <branch-name> # master로 브랜치 병합
$ git branch # 브랜치 전체보기
$ git log
```

merge를 진행하다 보면 병합 과정에서 conflict(충돌)이 발생할 수 있습니다.  
아래 명령어로 충돌 원인을 알 수 있습니다.

```
# conflict  (non fast-forward)
$ git status  //충돌난 이유를 알 수 있다.
```

충돌이 발생했다면 파일 수정 -> commit -> push 작업을 수행하면 해결할 수 있습니다.

### merge와 checkout -p 차이점

- checkout 시 -p 옵션을 주면 Patch 형태로 동작한다. 따라서 다른 브랜치의 특정 파일을 현재 브랜치의 파일로 패치할 수 있다. 다만 이 기능은 merge가 아니라 패치이므로 현재 브랜치의 수정 내용과는 관계없이 해당 파일의 내용으로 변경된다.
- merge는 패치와는 달리 현재 브랜치의 수정 내용과 다른 브랜치의 수정 내용을 합치는 것을 말한다. 이 과정에서 충돌이 발생할 수 있습니다.
