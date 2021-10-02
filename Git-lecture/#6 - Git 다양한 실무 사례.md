# Git 다양한 실무 사례

1. Remote에 올라간 파일/폴더 삭제
2. 실수로 master 브랜치에서 작업
3. 실수로 작업중인 브랜치를 삭제
4. 특정 태그로 긴급 롤백 & 다시 hotfix

## 1. Remote에 올라간 파일/폴더 삭제
실수로 remote repository에 불필요한 파일/폴더를
Push했다. 
.gitignore에 추가하고 삭제 후 push해도 원격에서는 지워지지 않는다.
```
1. 로컬과 리모트 모두 지우고 싶다. (media2)
$ git rm -r media2

2. 로컬에는 남겨두고 리모트에서만 지우고 싶다. 
$ git rm -r --cached media
```
## 2. 실수로 master 브랜치에서 작업
실수로 작업(Topic) 브랜치가 아닌 메인(Master) 브랜치에서 작업하고 커밋했다.
Master는 원위치하고, 작업한 소스는 살리고 싶다!!

두 가지 경우

1. 다행히 PUSH는 하지 않았다.
```
# 임시 브랜치 하나를 master에서 따옵니다.
$ git branch tmp

# master에서 commit전으로 reset합니다. 
$ git rest --hard HEAD ~

# 작업 브랜치에서 임시브랜치를 merge합니다.
$ git merge --no-ff tmp

#임시 브랜치는 삭제합니다.
$ git branch -d tmp
```
2. PUSH까지 해버렸다. 
```
# master에서 임시 브랜치를 생성합니다.
$ git branch tmp

# master를 commit 전으로 reset 합니다.
$ git reset --hard HEAD~

#서버에 강제 푸시합니다.
$ git push -f origin master

# 작업 브랜치로 가서 임시 브랜치를 merge합니다.
$ git merge --no-ff tmp
```
## 3. 실수로 작업 중인 브랜치를 삭제

작업 중이던 Topic 브랜치를 실수로 삭제했다. (-D)
git reset으로 브랜치는 복구되지 않는다.

```
# 브랜치를 그대로 복원하고 싶다.
$ git checkout -b <브랜치명> <revision 번호>
```
## 4. 특정 태그로 긴급 롤백 & 다시 hotfix

버그 수정(hotfix)해서 Tag 0.2.1 배포 후 

1. 예기치 못한 장애가 발생했다. 얼른 0.2.0으로 Rollback 하고 다시 배포하자! (git flow 사용하지 않으면 임시 브랜치를 만든다.)
```

# 0.2.0의 버그를 수정한 코드0.2.1을 임시 브랜치에 저장합니다.
$ git branch tmp

#태그 0.2.0으로 Rollback
$ git reset --hard 0.2.0

# Rollback 서버에 push
$ git push -f origin master
```
2. 태그 0.2.1의 소스를 이용해서 0.2.2를 작업하자. (git flow 사용)
```

# hotfix는 무조건 master 브랜치에서 나온다.
# hotfix에 master의 0.2.0 코드가 들어있다.
$ git flow hotfix start 0.2.2

# hotfix/0.2.2에 develop의 0.2.1 코드를 merge합니다. 
$ git merge --no-ff develop

# 수정이 완료되면 hotfix를 finish해서 master과 develop에 merge합니다.
$ git flow hotfix finish 0.2.2

모든 수정부분과 태그들을 서버에 push
$ git push origin --all --follow-tags
```