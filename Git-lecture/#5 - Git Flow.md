# Git Flow
## Git Flow ConcePts
기본 브랜치 
- Master : 항상서비스가능한 소스코드
- Develop: 개발에 주축이되는 브랜치

기능을 개발할때
- Feature/

배포를 할때
- Release/

긴급 버그를 수정하고 싶을때
- Hotfix/

## Git Flow Commands
```
$> git flow init
$> git push origin --all
$> git flow feature start <feature-branch>
$> git flow feature list
$> git add .
$> git commit -m
# push & pull-request(to review)
$> git flow feature finish <feature-branch>
$ other-feature> git merge --no-ff develop
$> git flow release start <tag>
$> git flow release finish <tag>
$> git tag
$> git push origin --all --follow-tags
$> git flow hotfix start <tag>
$> git flow hotfix finish <tag>
```

## Ex. Try This
1. 2개 feature 시작 (login, regist)
2. login, regist 각각 코딩
3. login 작업 완료
4. login 코드 리뷰
5. login 릴리즈 & 배포 (0.1.0)
7. regist 작업완료
8. regist 릴리즈 (0.2.0)
9. 0.1.0에서 버그 발생!! → hotfix 시작
10. hotfix 0.1.1 작업완료
11. hotfix 0.1.1 코드리뷰
12. hotfix 0.1.1 배포(0.1.1)
13. regist 릴리즈 마무리 & 배포(0.2.0)

![](../img/gitflow.PNG)