## 내가 보려고 적는 MongoDB 명령어 모음

### 시작

* `mongod --dbpath C:\mongodb\test`
* `mongo localhost:27017` 



### 상태확인

* `show dbs` : 데이터베이스 목록
* `show collections` : 컬렉션 목록
* `db.컬렉션이름.stats()` : 컬렉션 통계
* `db.stats()` : 데이터베이스 통계



### 컬렉션

* `use DB이름` : DB 생성 및 이동
* `db.createCollection{"이름", {capped: true, size: 10000 }}` : Capped 컬렉션 생성
* `db.컬렉션이름.renameCollection("바꿀컬렉션이름")` : 컬렉션 이름 변경



### 삭제

* `db.컬렉션이름.drop()` : 컬렉션 삭제
* `db.dropDatabase()` : 데이터베이스 삭제
* `db.컬렉션이름.deleteMany({})` : 모든 도큐먼트 삭제



### 조회

* `db.컬렉션이름.find( <query>, <projection> )` : projection은 내가 보고 싶은 것만 볼 수 있게 (false 지정해서)



### 수정

* `db.컬렉션이름.replaceOne( <query>, <replacement> {upsert: <boolean>, writeConcern: <document>, collation: <document>})` : 도큐먼트 교체
  * replacement에 대체할 내용
  * upsert가 true면 쿼리한 도큐먼트가 없을 때 추가
  * collation : 악센트나 대소문자 관계에 대한 순서 설정

* `db.컬렉션이름.updateOne( <query>, <update>, {upsert: <boolean>, writeConcert: <document>, collation: <document>, arrayFilters: [<filterdocument1>, ... ] } )` : 도큐먼트 수정
  * update에 적용할 변동사항
  * arrayFilters : 지정된 배열 필드에서 업데이트 작업을 위해 수정할 배열 요소를 결정하는 필터 문서 배열
* 도큐먼트 수정 연산자
  * `$set` : 정해진 필드의 값 변경
  * `$inc` : 필드 값 증가시킴
  * `$currentDate` : 필드 값을 현재의 timestamp나 date 값을 갖도록 추가
  * `$min`, `$max` : 필드 값이 주어진 값 이하/이상이면 주어진 값으로 설정
  * `$mul` : 필드값에 곱하기
  * `$rename` : 필드 이름 변경