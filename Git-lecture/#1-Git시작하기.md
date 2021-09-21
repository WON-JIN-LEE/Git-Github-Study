# Git 시작하기

## Git 환경 설정

- 바탕화면 git bash 실행
- git config --list
- git config user.name
- git config --global user.name <github-name>
- git config user.email
- git config --global user.email <email>
- git config 한눈에 보기
- cat ~/.gitconfig

--global 이 들어가면 컴퓨터 전역에 설정한다. 반복 수행 할 필요가 없어진다.

## 로컬 저장소 만들기

- cd "work-dir"
- git init
- .gitignore 파일 작성
- git add --all
- git add <file명> 또는 git add .
- git commit -m "first commit message"
- git remote add origin <git-remote-url>
- git push -u origin master // -u: 현재 브랜치를 자동으로 서버 master 브랜치로 연결해 간단히 git push, git pull만 입력해도 명령어를 반영한다.
- git push -fu origin master //충돌이 나도 무시하고 보낸다. -fu
- git log
- git status # staging 상태 확인

(참고) GibHub RemoteURL 패턴 : https://github.com/<사용자이름>/<저장소명>.git

### 주의할 점

- 팀원이 코드를 수정하거나 커밋했을 때 서버 레파지토리를 먼저 pull로 코드를 동기화해야 합니다. 그 다음에 push해야 reject가 발생하지 않습니다.

## git clone & pull 하는 방법

- git clone "github-remote-url" // GitHub에 만든 repo와 클론하기
- git pull : 서버의 최신 소스를 다운받기
- touch aaa.txt
- git add --all
- git commit -am “message”
- git push

(참고: 서버와 연결된 repo 끊기): git remote rm origin
