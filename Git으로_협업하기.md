# Git으로 협업하기

> 깃허브로 여러 사람과 함께 협업하는 방법 정리



## Wiki

> 문서는 레포의 Wiki 탭에서 관리



## Pull request

> "내가 작업한 브랜치를 원본으로 Pull 해주세요!" 하고 요청을 보내는 것
>
> 내가 작성한 코드가 아무 리뷰없이 master 브랜치로 push되는 것 방지!



### Pull request 하는 법

1. Fork

   * 원본 레포(hijinkim/NarangSalGae)를 본인의 레포로 `Fork` 하기
   * 본인 레포를 `git clone` 하기
   * 원본 프로젝트를 저장할 저장소 추가 `git remote add 이름 원본레포주소`
   * `git remote -v` 했을 때 origin으로 본인의 레포의 fetch와 push, 위에서 지정한 이름으로 된 원본 레포의 fetch와 push 총 4개의 주소가 보여야함

2. branch 생성

   * 로컬에서 작업할 때는 브랜치 생성하여 작업
   * 브랜치 생성: `git checkout -b 브랜치이름`
   * 브랜치 확인: `git branch`
   * 브랜치 이동: `git checkout 브랜치이름`

3. 코드 작성, push

   * 코드 작성 후 add, commit 진행

   * push는 `git push origin 브랜치이름` 으로 푸시

     ~~-u 옵션을 주면 git push만 입력해도 알아서 브랜치로 수정사항이 반영된다고 하는데 잘 모르겠음~~

4. Pull request 생성

   * push 후 깃허브를 보면 `Compare & pull request` 버튼 활성화 혹은 Pull request 탭으로 이동
   * 제목은 해결방안 위주, 메시지 작성 후 PR

5. Merge 이후 branch 삭제하기

   * Merge가 되면 `pull`을 통해 원본저장소와 로컬저장소를 동기화
   * 생성한 브랜치는 삭제
   * Merge는 PR 작성자가 직접 할 수 있음



### 리뷰

> Pull request를 하면 코드에 대한 리뷰가 가능

* comment : 코멘트
* request changes : 코드에서 버그가 발견되어 수정 요청
* approve : merge 동의



* Pull request에서 `Add your review`로 리뷰 추가 가능
* comment나 request changes 요청을 하면 Merge 승인 X



## Issues

> 프로젝트를 진행하며 의견이 필요한 모든 상황이 이슈!
>
> 이슈를 등록하면 이슈를 기반으로 작업 진행
>
> 효율적인 관리 위해 태그 달기!



### labels

>  Issues의 labels 탭에서 라벨 관리 및 추가 가능
>
> 이슈 상세 화면에서 오른쪽 사이드 메뉴 통해 label 부여 가능
>
> assignees(책임자) 부여 가능
>
> `milestaone` : 이슈들의 그룹, 기능별 관련 유사 이슈들을 쉽게 찾기 위해, 상세 화면에서 사이드 메뉴 통해 부여 가능 (~~버전별, 기능별로 나누면 되는 것 같다~~)



## 칸반보드

> 역시 이슈를 효율적으로 관리하는데 도움이 되는 기능
>
> 이슈를 진행 중인 이슈, 완료된 이슈로 나눌 수 있고 우선 순위별 나열도 가능





## 참고 자료

https://m.blog.naver.com/thalsal/222203346666

https://velog.io/@hidaehyunlee/Github%EB%A1%9C-%ED%98%91%EC%97%85%ED%95%98%EA%B8%B0

https://uang.tistory.com/12

