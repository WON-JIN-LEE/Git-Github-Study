# Reset & Revert / conflict & merge

## Reset & Revert & Source History 명령어

Source History

- git log --graph --oneline

Reset

- git reset --[hard | soft | mixed] <revision번호>
  - (주의) hard는 시계(모든것)를 되돌림!!

Revert

- git revert <revision번호>
  - history쌓임, 소스 그대로

revision번호

- 아래사진에서 스크랩되어 있는 부분에 각 Log 마다 revision번호가 표시됩니다.

![](../img/revision.PNG)

---

## conflict & merge

conflict

<<<< HEAD (server와 충돌난 부분)
<br>>>>> local

editor에서 수정

저장 후 아래 명령 수행

- git add --all
- git commit -am "aaaaa"
- git log --graph --decorate --oneline
- git status
