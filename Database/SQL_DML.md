#### :book: 이것이 MariaDB다, 우재남, 한빛미디어 참고



# SQL_DML

> DML (Data Manipulation Language)
>
> 데이터베이스 사용자가 응용 프로그램이나 질의어를 통해 저장된 데이터를 실질적으로 관리하는데 사용되는 언어



## SELECT

```sql
SELECT select_expr
	[FROM table_references]
	[WHERE where_condition]
	[GROUP BY {col_name|expr|position}]
	[HAVING where_condition]
	[ORDER BY {col_name|expr|position}]
```



### SELECT

* `SELECT 열1, 열2, 열3` : 여러 개의 열 가져올 수 있음
* `SELECT *` : 모든 열 가져오기



### WHERE

* `WHERE age >= 20 AND height >= 150` : age가 20 이상이고 height가 150 이상 
* `WHERE 속성 BETWEEN age >= 20 AND height >= 150` : 연속적인 값만 가능 
* `WHERE addr='경기' OR addr='강원' OR addr='전북'` : addr가 경기, 강원, 전북인 경우
* `WHERE addr IN ('경기', '강원', '전북')` : 이산적인 값인 경우 
* `WHERE name LIKE '김%'` : 김으로 시작하는 name을 가진 경우
* `WHERE name LIKE '_희진'` : 맨 앞글자가 한 글자이고 그 다음이 희진인 경우
* `WHERE name LIKE '_용%'` : 맨 앞글자가 한 글자이고 그 다음 용 그 뒤에는 몇 글자든 상관 없음
  * %, _가 문자열의 맨 앞에 들어가는 것은 성능에 영향을 줌



### 서브쿼리

```sql
SELECT Name, height FROM userTbl
	WHERE height >= (SELECT height FROM userTbl WHERE name = '김희진');
```

* `WHERE height >= ANY (SELECT height FROM userTbl WHERE addr = '경남')` : 173보다 크거나 같은 사람, 170보다 크거나 같은 사람 출력 (서브쿼리가 둘 이상의 값 반환)
* `WHERE 속성 >= ALL (서브쿼리)` : 서브쿼리의 여러 결과를 모두 만족
* `SOME` 은 `ANY` 와 동일한 의미

* 조건 연산자 대신 `IN` 사용 가능

### ORDER BY

* `SELECT Name, mDate FROM userTbl ORDER BY mDate;` :  mDate를 기준으로 오름차순 정렬
* `SELECT Name, mDate FROM userTbl ORDER BY mDate DESC;` : 내림차순 정렬



### DISTINCT

* `SELECT DISTINCT addr FROM userTbl;`



### LIMIT

* `SELECT name FROM employees ORDER BY hire_date ASC LIMIT 5;`



### 테이블 복사

* `CREATE TABLE 새로운 테이블명 (SELECT 복사할 열 FROM 기존 테이블)`



### GROUP BY

* `SELECT userID, SUM(amount) FROM buyTbl GROUP BY userID;` : userID 별로 묶어 amount 개수 출력



### 집계 함수

|     함수명      |             설명             |
| :-------------: | :--------------------------: |
|      AVG()      |             평균             |
|      MIN()      |            최소값            |
|      MAX()      |            최대값            |
|     COUNT()     |          행의 개수           |
| COUNT(DISTINCT) | 행의 개수(중복은 1개만 인정) |
|     STDEV()     |           표준편차           |
|   VAR_SAMP()    |             분산             |

* `SELECT AVG(amount) AS '평균 개수'` : 별칭 사용
* 집계 함수는 WHERE절에서 사용할 수 없음



### HAVING

```sql
SELECT userID AS '사용자', SUM(price*amount) AS '총구매액'
	FROM buyTbl
	GROUP BY userID
	HAVING SUM(price*amount) > 1000;
```

* HAVING 절은 GROUP BY절 다음에 와야 함



### ROLLUP

```sql
SELECT groupName, SUM(price*amount) AS '비용'
FROM buyTbl
GROUP BY groupName
WITH ROLLUP;
```

* 총합, 중간 합계가 필요한 경우 GROUP BY절과 함께 WITH ROLLUP문 사용



## INSERT

```sql
INSERT [INTO] 테이블[(열1, 열2, 열3, ... )] VALUES (값1, 값2, 값3, ... )
```



### AUTO_INCREMENT

* AUTO_INCREMENT 지정할 때는 꼭 PRIMARY KEY 또는 UNIQUE 지정해야 함
* 데이터 형은 숫자 형식만 가능
* `SELECT LAST_INSERT_ID()` : 마지막에 입력된 AUTO_INCREMENT 값 보여줌
* `ALTER TABLE 테이블명 AUTO_INCREMENT=숫자` : 입력값을 원하는 숫자부터 입력되도록 변경
* `SET @@auto_increment_increment=숫자` : 증가값 원하는 숫자로 변경



### 다른 테이블에서 데이터 가져오기

* INSERT INTO ... SELECT문
* CREATE TABLE ... SELECT 문



### IGNORE

> 기본 키가 중복된 데이터를 입력하려고 하면 입력되지 않는다. 
>
> 한 건의 오류때문에 나머지 데이터도 입력되지 않는 문제가 발생할 수 있다. 
>
> 이럴 경우 IGNORE를 사용하면 된다.

```sql
INSERT IGNORE INTO memberTbl VALUES ('A', '가', '1');
INSERT IGNORE INTO memberTbl VALUES ('B', '나', '2');
INSERT IGNORE INTO memberTbl VALUES ('C', '다', '3');
```

첫 번째 항목 ('A', '가', '1') 이 기본키가 중복된 데이터를 입력하여 오류가 발생하여도 두 번째와 세 번째 항목은 정상 입력된다.



### ON DUPLICATE

> 입력 시 기본 키가 중복되면 데이터를 수정하기

```sql
INSERT INTO memberTbl VALUES('A', '가', '1')
ON DUPLICATE KEY UPDATE name = '가가가', addr = '1';
```

기본키가 중복될 경우 이미 있는 데이터의 name, addr을 '가가가', '1' 으로 변경

중복이 아닌 경우 그냥 삽입



## DELETE

```sql
DELETE FROM 테이블이름 WHERE 조건;
```

* 조건 없으면 전체 데이터 삭제



## UPDATE

```sql
UPDATE 테이블이름
SET 열1 = 값1, 열2 = 값2
WHERE 조건;
```

* WHERE 생략할 경우 전체 테이블의 내용 변경



## WITH, CTE

> CTE (Common Table Expression) : 기존의 뷰, 파생 테이블, 임시 테이블 등으로 사용되던 것 대신 함, 더 간결하게 보여짐
>
> WITH 절은 CTE를 표현하기 위한 구문



### 비재귀적 CTE

```sql
WITH CTE_테이블이름(열이름)
AS
(
	<쿼리문>
)
SELECT 열이름 FROM CTE_테이블이름;
```



예시

```sql
WITH cte_userTBL(addr, maxHeight)
AS
	( SELECT addr, MAX(height) FROM userTBL GROUP BY addr )
SELECT AVG(maxHeight * 1.0) AS '각 지역별 최고키 평균' FROM cte_userTBL;
```



### 중복 CTE

```sql
WITH
AAA (컬럼들)
AS (AAA의 쿼리문),
	BBB (컬럼들)
	AS (BBB의 쿼리문),
		CCC (컬럼들)
		AS (CCC의 쿼리문)
SELECT * FROM [AAA 또는 BBB 또는 CCC]
```

* CCC의 쿼리문에서는 AAA나 BBB 참조 가능
* AAA 쿼리문이나 BBB 쿼리문에서는 CCC 참조 불가능
* 아직 정의되지 않은 CTE 미리 참조할 수 없음