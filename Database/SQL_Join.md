#### :book: 이것이 MariaDB다, 우재남, 한빛미디어 참고



# SQL Join

> 조인이란 두 개 이상의 테이블을 서로 묶어서 하나의 결과 집합으로 만들어 내는 것



## INNER JOIN

> 양쪽 테이블에 모두 내용이 있는 것만 조인되는 방식

```sql
SELECT <열 목록>
FROM <첫 번째 테이블>
	INNER JOIN <두 번째 테이블>
	ON <조인될 조건>
[WHERE 검색 조건]
```

```sql
SELECT B.userID, U.name, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2) AS '연락처'
	FROM buyTBL B
		INNER JOIN userTBL U
			ON B.userID = U.userID;
-- 테이블에 별칭 주기
```



## OUTER JOIN

> 조인 조건에 만족되지 않는 행까지도 포함시키는 것

```sql
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
	<LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이플)>
		ON <조인될 조건>
	[WHERE 검색 조건];
```

* LEFT OUTER JOIN : 왼쪽 테이블의 것은 모두 출력되어야 한다
* RIGHT OUTER JOIN : 오른쪽 테이블의 것은 모두 출력되어야 한다.
* FULL OUTER JOIN : 양쪽 모두에 조건이 일치하지 않는 것을 모두 출력 (LEFT OUTER JOIN + RIGHT OUTER JOIN)



## CROSS JOIN

> 한쪽 테이블의 모든 행들과 다른쪽 테이블의 모든 행을 조인시키는 기능
>
> CROSS JOIN 결과 개수는 두 테이블 개수 곱한 것
>
> 카티션곱

```sql
SELECT *
	FROM <테이블1>
	 CROSS JOIN <테이블2>
```



## SELF JOIN

> 자기 자신과 자기 자신이 조인
>
> 하나의 테이블에 같은 데이터가 존재하되 의미는 다르게 존재하는 경우

```sql
SELECT <열 목록>
	FROM <테이블명>
		INNER JOIN <테이블명>
			ON <조인될 조건>
```



## UNION / UNION ALL / NOT IN / IN

```sql
SELECT 문장1
	UNION [ALL]
SELECT 문장2
```

* UNION : 중복된 열은 제거, 데이터 정렬되어 나옴
* UNION ALL : 중복된 열까지 모두 출력
* NOT IN : 첫 번째 쿼리의 결과에서 두 번째 쿼리에 해당하는 것을 제외
* IN : 첫 번째 쿼리의 결과에서 두 번째 쿼리에 해당하는 것만 조회