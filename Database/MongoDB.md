#### :book: 맛있는 MongoDB, 정승호, 비제이퍼블릭



# MongoDB

> 비관계형(NoSQL) DBMS
>
> 장점 : 빠른 속도, 확장성, 친숙함, 이용의 편리성, 쉽고 빠른 분산 컴퓨팅 환경 구성



## 데이터 타입

> 도큐먼트는 BSON(Binary JSON) 구조로 이루어짐



### BSON 값

|  타입   |              설명              |   종류    |              예시              |
| :-----: | :----------------------------: | :-------: | :----------------------------: |
|  Null   |    아무것도 없는 것을 의미     |   null    |              null              |
| 정수형  |         정수 값을 가짐         | int, long |            1, 1000             |
| 실수형  |         실수 값을 가짐         |  double   |              1.23              |
| 문자열  |        문자 정보를 가짐        |  string   |        "hello", 'hello'        |
| Object  | 정보를 필드와 값의 형태로 가짐 |  object   | {field : 'value', number : 1}  |
|  Array  |   정보를 배열의 형태로 가짐    |   array   | [1, 2.34, null, {x : 1}, true] |
| Boolean |     참과 거짓에 대한 정보      |  boolean  |          true, false           |

* 오브젝트 : 임베디드 도큐먼트라고 불림, 도큐먼트 내부의 값으로 도큐먼트를 가짐
* 배열 : 배열 요소로 여러 가지 자료형 가질 수 있음, 배열 안에 여러 도큐먼트 저장 가능 (배열 속 임베디드 도큐먼트)



### 타임스탬프

* `Timestamp(1412180887, 1)` : (유닉스 시간, 같은 유닉스 시간 내에서 몇 번째인지)



### 날짜

* `ISODate("2020-01-22T11:00:00.123Z")` : (날짜T시각)

* `new Date(dateString)` : 날짜 및 시간 형식의 문자열 생성
* `new Date(year, monthIndex[, day[, hour[, minutes[, seconds[, milliseconds]]]]])` : 년도, 일, 시간, 분, 초, 밀리초를 파라미터로 넘겨서 생성



### ObjectID

* `ObjectID("542c2b97 bac059 5474 108b48")` : (유닉스 시간, 기기id, 프로세스id, 카운터)
  * 컬렉션 안에 도큐먼트 생성할 때마다 _id 필드 자동 생성 (Primary key)



## 컬렉션, 데이터베이스

### 데이터베이스, 컬렉션 삭제와 수정

```javascript
db.dropDatabase() // 현재 데이터베이스 삭제
db.collection.drop() // collection 삭제
db.collection.renameCollection(바꿀이름) // collection의 이름 변경
```



### Capped 컬렉션

```javascript
db.createCollection(<컬렉션 이름>, { capped: true, size: <제한할 크기>}) // Capped 컬렉션 생성
```

* Capped 컬렉션 : 정해진 크기를 초과하게 되면 자동으로 가장 오래된 데이터를 삭제
* 로그 데이터, 일정 시간 동안만 보관하는 통계 데이터를 보관할 때 유용



### 데이터베이스, 컬렉션 상태 조회

```javascript
db.getCollectionInfos() // 현재 데이터베이스의 컬렉션들의 정보를 리스트로 반환 (이름, 타입, UUID)
db.serverStatus() // 호스트, 프로세스id, Lock 옵션, 스토리지 엔진 이름, 스토리지 엔진 통계 정보 제공
db.stats() // 데이터베이스 내 컬렉션, 뷰, 오브젝트 개수와 크기에 대한 통계 제공

db.colleection.isCapped() // 컬렉션이 Capped 컬렉션이면 true 반환
db.collection.latencyStats() // 컬렉션의 지연 시간 통계
db.collection.stats() // 컬렉션의 크기, 도큐먼트 개수, 스토리지 엔진의 통계 제공
db.collection.storageSize() // 컬렉션 스토리지의 크기 반환
db.collection.totalIndexSize() // 컬렉션의 인덱스 크기 반환
db.collection.totalSize() // 컬렉션의 스토리지와 인덱스 크기의 합
```



### 도큐먼트 생성

```javascript
db.user.insertOne({username:"karoid", password:"1111"}) // 단일 도큐먼트 생성

db.collection.insertOne(
	<document>,
    {
    	writeConcern: <document>
    }
)
```

* WriteConcern : insertOne 명령어가 도큐먼트를 컬렉션에 넣으려고 할 때 이미 이 컬렉션이 쓰기 작업을 하고 있다면 어떤 영향을 줄지 설정하는 것



```javascript
db.collection.insertMany( // 둘 이상의 도큐먼트를 컬렉션에 생성
	[<document 1>, <document 2>, ... ],
    {
        writeConcern : <document>,
        ordered : <boolean>
    }
)
```

* ordered : 선택적, 순서대로 입력할지 상관없을지, 기본값은 true
* 생성 시 에러 발생한 경우 : `BulkWriteError`
  * nInserted : 도큐먼트 생성에 성공한 횟수
  * nUpserted : 도큐먼트 upsert에 성공한 횟수
  * nMatched : 도큐먼트 조회에 성공한 횟수
  * nRemoved : 도큐먼트 제거에 성공한 횟수
  * upserted : upsert 작업이 완료된 도큐먼트에 대한 정보



### 도큐먼트 조회

```javascript
db.user.find( <query>, 
<projection>
)
```

* query : 선택적, 쿼리 연산자를 이용해 원하는 도큐먼트 선택
* projection : 선택적, return 할 필드를 선택할 수 있음













