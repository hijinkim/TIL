# Git

버전을 통해 코드 관리하는 도구, 협업 도구

* SCM : Source Code Management, 코드 관리
* VCS : Version Control System, 버전 관리

Git은 폴더 단위로 프로젝트/코드를 관리



## Git 명령어

* `git init` : initialize, git으로 코드 관리를 시작
  * `(master)`가 프롬프트에 표시
  * `.git` 폴더 생성
* `git config -global user.name '사용자 이름'` : 초기 설정
* `git config -global user.email '사용자 이메일'` : 초기 설정

* `git status` : git의 상태를 출력
* `git add [파일명]` : git이 스냅샷을 찍기 위해 추적하는 리스트에 파일 추가
* `git commit -m '커밋 메시지'` : git을 통해 스냅샷을 찍음 (==버전을 만듦, 현재 상태 저장)
* `git log` : git으로 지금까지 저장된 커밋들의 로그 출력
  * `git log --oneline` : 한 줄로 커밋을 출력
  * `git log -[숫자]` : 입력된 숫자만큼 역순으로 출력
* `git restore --staged [파일명]` : staging area에 추가된 파일을 복원시키는 것

* `git remote` : 현재 관리되고 있는 원격 저장소 정보 출력
  * `git remote -v` : verbose mode, 주소까지 상세 정보 출력
* `git remote add [원격저장소 이름] [원격저장소 주소]` : 새로운 원격 저장소 정보 추가
  * `git remote add origin https://github.com/유저이름/저장소이름`
* `git remote remove [원격저장소 이름]` : 해당 원격저장소 정보 삭제
* `git push [원격저장소 이름] [브랜치 이름]` : 원격저장소에 코드 업로드
  * `git push -u origin master` : upstream 설정
* `git clone [원격저장소 주소] (폴더명)` : 원격저장소의 코드 다운로드
* `git bash` : 현재 생성되어 있는 branch 목록 출력

* `git branch [브랜치 이름]` : 새로운 branch 생성

* `git branch -d [브랜치 이름]` : delete, branch 삭제, 병합된 branch는 항상 삭제
* `git checkout [브랜치 이름]` : 해당 branch로 이동

* `git merge [브랜치 이름]` : branch 병합 (현재 속한 브랜치에서 인자로 주어진 브랜치 합병)
* `git checkout --[파일 이름]` : stage 되지 않은 modified된 파일을 수정 이전의 상태로 되돌리기