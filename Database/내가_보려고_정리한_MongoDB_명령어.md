## 내가 보려고 적는 MongoDB 명령어 모음

### 시작

* `mongod --dbpath 'C:\mongodb\test'`
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



