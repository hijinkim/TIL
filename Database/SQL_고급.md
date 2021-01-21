#### :book: 이것이 MariaDB다, 우재남, 한빛미디어 참고



# SQL 고급



## MariaDB 데이터형식

### 숫자 데이터 형식

|   데이터 형식   | 바이트 수 |       숫자 범위        |                설명                |
| :-------------: | :-------: | :--------------------: | :--------------------------------: |
|    SMALLINT     |     2     |    -32,768 ~ 32,767    |                정수                |
|       INT       |     4     |    약 -21억 ~ 21억     |                정수                |
|     BIGINT      |     8     |   약 -900경 ~ 900경    |                정수                |
|      FLOAT      |     4     | -3.40E+38 ~ -1.17E-38  |       소수점 아래 7자리까지        |
|     DOUBLE      |     8     | -1.22E-308 ~ 1.79E+308 |       소수점 아래 15자리까지       |
| DECIMAL(m, [d]) |   5~17    |   -10^38+1 ~ 10^38-1   | 전체 자릿수m와 소수점 이하 자리수d |



### 문자 데이터 형식

| 데이터 형식 |   바이트 수    |           설명           |
| :---------: | :------------: | :----------------------: |
|   CHAR(n)   |    1 ~ 255     |     고정길이 문자형      |
| VARCHAR(n)  |   1 ~ 65535    |     가변길이 문자형      |
|  LONGTEXT   | 1 ~ 4294967295 | 최대 4GB의 TEXT 데이터값 |
|  LONGBLOB   | 1 ~ 4294967295 | 최대 4GB의 BLOB 데이터값 |

* CHAR 형식은 10자리 지정 후 3자리만 쓰면 7자리 낭비
* VARCHAR 형식은 10자리 지정 후 3자리만 쓰면 3자리만 사용
* 하지만 CHAR 형식이 INSERT, UPDATE 시 일반적으로 더 좋은 성능
* LONGTEXT, LONGBLOB 형식은 데량의 데이터 저장
* LONGBLOB은 바이너리 파일



### 날짜, 시간 데이터 형식

| 데이터 형식 | 바이트 수 |           설명           |
| :---------: | :-------: | :----------------------: |
|    DATE     |     3     |     YYYY-MM-DD 형식      |
|  DATETIME   |     8     | YYYY-MM-DD HH:MM:SS 형식 |



### 변수 사용

```sql
SET @변수이름 = 변수값; -- 변수 선언 및 값 대입
SELECT @변수이름; -- 변수 값 출력
```



```sql
SET @myVar1 = 3;
PREPARE myQuery
	FROM 'SELECT Name, height FROM userTBL ORDER BY height LIMIT ?';
EXECUTE myQuery USING @myVar1;
```

* LIMIT에는 원칙적으로 변수 사용 불가능, PREPARE, EXECUTE문을 활용하여 변수 활용 가능
* `PREPARE 쿼리이름 FROM '쿼리문'` 은 쿼리문을 준비만 해뒀다가 EXECUTE 쿼리를 만나면 실행
* `USING @변수` 를 이용해서 쿼리문에서 ?으로 처리해놓은 부분에 대입



### 데이터 형식 형 변환

```sql
CAST ( expression AS 데이터형식 [(길이)])
CONVERT (expression, 데이터형식 [(길이)])
```

```sql
-- 정수 형변환 예시
SELECT CAST(AVG(amount) AS SIGNED INTEGER) AS '평균 구매 개수' FROM ... ;
SELECT CONVERT(AVG(amount) AS SIGNED INTEGER) AS '평균 구매 개수' FROM ... ;

-- 날짜 형식 변환 예시
SELECT CAST('2020$01$20' AS DATE); -- $, /, %, @ 가능

-- 쿼리 결과 보기 좋게 표현, CONCAT는 문자열 연결해주는 함수
SELECT num, CONCAT(CAST(price AS CHAR(10)), 'X', CAST(amount AS CHAR(4)), '=') AS '단가X수량', 
	price*amount AS '구매액'
FROM ... ;
```



### 암시적 형 변환

```sql
SELECT '100' + '200'; -- 300, 정수로 변환되어 연산
SELECT CONCAT('100', '200'); -- 100200
SELECT CONCAT(100, '200'); -- 100200, 정수가 문자로 변환
SELECT 1 > '2mega'; -- 0(False), 정수 2로 변환
SELECT 3 > '2MEGA'; -- 1(True), 정수 2로 변환
SELECT 0 = 'mega2'; -- 1(True), 문자는 0으로 변환
```



## MariaDB 내장 함수

### 제어 흐름 함수

* IF(수식, 참, 거짓)

```sql
SELECT IF (100 > 200, '참이다', '거짓이다')
```

* IFNULL(수식1, 수식2)

```sql
SELECT IFNULL(NULL, '널값이다') IFNULL(100, '널값이다')
-- 널값이다, 100
```

* NULLIF(수식1, 수식2)

```sql
SELECT NULLIF(100, 100), NULLIF(200, 100)
-- NULL, 200
-- 수식1과 수식2가 같으면 NULL, 다르면 수식1 반환
```

* CASE WHEN ELSE END

```sql
SELECT 	CASE 10
		WHEN 1 THEN 'ONE'
		WHEN 5 THEN 'FIVE'
		WHEN 10 THEN 'TEN'
		ELSE 'X'
	END;
-- TEN
```



### 문자열 함수

* ASCII, CHAR

```sql
SELECT ASCII('A'), CHAR(65);
-- 65, 'A'
```

* BIT_LENGTH(문자열), CHAR_LENGTH(문자열), LENGTH(문자열)

```sql
SELECT BIT_LENGTH('abc'), CHAR_LENGTH('abc'), LENGTH('abc');
-- 3byte, 3, 3byte
-- 한글은 한 글자 3byte
```

* CONCAT(문자열1, 문자열2), CONCAT_WS(구분자, 문자열1, 문자열2)

```sql
SELECT CONCAT_SW('/'. '2021', '01', '20');
-- 2021/01/20
```

* ELT(위치, 문자열1, 문자열2) 
* FIELD(찾을 문자열, 문자열1, 문자열2)
* FIND_IN_SET(찾을 문자열, 문자열 리스트)
* INSTR(기준 문자열, 부분 문자열)
* LOCATE(부분 문자열, 기준 문자열), POSITION()

```sql
SELECT 	ELT(2, '하나', '둘', '셋'), -- 둘, 위치 번째에 해당하는 문자열 반환
		FIELD('둘', '하나', '둘', '셋'), -- 2, 찾을 문자열의 위치 반환, 없으면 0
		FIND_IN_SET('둘', '하나,둘,셋'), -- 2, 찾을 문자열을 문자열 리스트에서 찾아 위치 반환
										-- 문자열은 콤마로 구분, 공백 없어야 함
		INSTR('하나둘셋', '둘'), -- 3, 기준 문자열에서 부분 문자열 찾아 시작 위치 반환
		LOCATE('둘', '하나둘셋'); -- 3, INSTR()과 동일하지만 파라미터 순서 반대
```

* FORMAT(숫자, 소수점 자릿수)

```sql
SELECT FORMAT(123456.123456, 4);
-- 123,456.1235
```

* BIN(숫자), HEX(숫자), OCT(숫자)

```sql
SELECT BIN(31), HEX(31), OCT(31);
-- 11111, 1F, 37
```

* INSERT(기준 문자열, 위치, 길이, 삽입할 문자열)

```sql
SELECT INSERT('ABCDEFG', 3, 4, '@@@@'), INSERT('ABCDEFG', 3, 2, '@@@@');
-- AB@@@@G, AB@@@@EFG
```

* LEFT(문자열, 길이), RIGHT(문자열, 길이)

```sql
SELECT LEFT('ABCDE', 3), RIGHT('ABCDE', 3);
-- ABC, CDE
```

* UPPER(문자열), UCASE('문자열'), LOWER(문자열), LCASE('문자열')

* LPAD(문자열, 길이, 채울 문자열), RPAD(문자열, 길이, 채울 문자열)

```sql
SELET LPAD('가나다', 5, '##');
-- ##가나다
```

* LTRIM(문자열), RTRIM(문자열) : 왼쪽/오른쪽 공백 제거
* TRIM(문자열), TRIM(방향 자를문자열 FROM 문자열) : 앞뒤 공백 제거

```sql
SELECT TRIM(BOTH 'Z', FROM 'ZZZabcZZZ');
-- abc
-- BOTH 양쪽, LEADING 앞, TRAILING 뒤
```

* REPEAT(문자열, 횟수) : 반복
* REPLACE(문자열, 원래 문자열, 바꿀 문자열) : 대체
* REVERSE(문자열) : 문자열 순서 거꾸로
* SPACE(길이) : 길이만큼 공백 반환
* SUBSTRING(문자열, 시작위치, 길이), SUBSTRING(문자열 FROM 시작위치 FOR 길이) : 시작 위치부터 길이만큼 반환
* SUBSTRING_INDEX(문자열, 구분자, 횟수) : 문자열에서 구분자가 횟수 번째 나오면 그 후 오른쪽은 버림

```sql
SELECT SUBSTRING_INDEX('cafe.naver.com', '.', 2)
-- cafe.naver
```





### 수학 함수

* ABS() : 절대값
* ACOS(), ASIN(), ATAN(), ATAN2(), SIN(), COS(), TAN() : 삼각함수
* CEILING(), FLOOR(), ROUND() : 올림, 내림, 반올림
* CONV(숫자, 원래 진수, 변환할 진수) : 진수 변환
* DEGREES(), RADIANS(), PI() : 각도값, 라디안값 변환, 파이값 반환
* EXP(), LN(), LOG(), LOG2(), LOG10() : 지수, 로그
* MOD(), 숫자1 % 숫자2, 숫자1 MOD 숫자2 : 나머지 연산
* POW(), SQRT() : 거듭제곱, 제곱근
* RAND() : 0 ~ 1 랜덤 실수
* FLOOR(m + (RAND() * (n - m))) : m <= 랜덤 수 < n
* SIGN() : 양수인지 0인지 음수인지, 1 / 0 / -1 반환
* TRUNCATE() : 숫자를 소수점 기준으로 정수까지 구하고 버림

```sql
SELECT TRUNCATE(12345.12345, -2) 
-- 12300
```



### 날짜, 시간 함수

* ADDDATE(날짜, 차이), SUBDATE(날짜, 차이) : 날짜 기준으로 차이를 더하거나 뺀 날짜
* ADDTIME(날짜/시간, 시간), SUBTIME(날짜/시간, 시간) : 날짜/시간 기준으로 시간을 더하거나 뺀 결과
* CURDATE(), CURTIME(), NOW(), SYSDATE() : 현재 날짜, 시간
* YEAR(), MONTH(), DAY(), HOUR(), MINUTE(), SECOND(), MICROSECOND()
* DATE(), TIME()
* DATEDIFF(날짜1, 날짜2), TIMEDIFF(날짜/시간, 날짜/시간) : 날짜 - 날짜, 시간 - 시간
* DAYOFWEEK(날짜), MONTHNAME(), DAYOFYEAR(날짜) : 요일 및 1년 중 몇 번째 날인지
* LAST_DAY() : 주어진 날짜의 마지막 날짜
* MAKEDATE(연도, 정수) : 연도에서 정수만큼 지난 날짜
* MAKETIME(시, 분, 초)
* PERIOD_ADD(연월, 개월수), PERIOD_DIFF(연월, 연월): 연월 + 개월, 연월 - 연월
* QUARTER(날짜) : 분기 반환
* TIME_TO_SEC(시간) : 시간을 초단위로 반환



### 시스템 정보 함수

* USER(), DATABASE()
* FOUND_ROWS() : 바로 앞 SELECT  문에서 조회된 행의 개수
* ROW_COUNT() : 바로 앞 INSERT, UPDATE, DELETE 문에서 입력, 수정 삭제된 행의 개수
* VERSION()
* SLEEP()



## 윈도우 함수

> 행과 행 사이의 관계를 쉽게 정의하기 위해서 제공되는 함수



### 순위함수

* RANK() : 공동 n등이 m명이면 그 다음 순위는 n + m 등
* NTILE() : 그룹으로 나누기
* DENSE_RANK() : 순위가 동일할 경우 같은 등수로 처리
* ROW_NUMBER() 

```sql
<순위함수이름>() OVER(
	[PARTITION BY <partition_by_list>]
	ORDER BY <order_by_list>)
```



### 분석함수

* CUME_DIST() : 백분율
* LEAD() : 다음 행
* FIRST_VALUE() : 그룹 내 가장 큰 값
* LAG() : 이전 행
* LAST_VALUE() : 그룹 내 가장 작은 값
* PERCENT_RANK() : 백분율



## 피벗, JSON

### 피벗

> 한 열에 포함된 여러 값을 출력하고 이를 여러 열로 변환하여 테이블 반환 식을 회전하고 필요한 경우 집계까지 수행하는 것



### JSON 데이터

> 현대의 웹과 모바일 응용프로그램 등과 데이터를 교환하기 위한 개방형 표준 포맷
>
> 속성과 값으로 쌍을 이루며 구성

```sql
SET @json = '{ "userTBL" :
[
    {"name" : "임재범", "height" : 182},
    {"name" : "이승기", "height" : 182},
    {"name" : "성시경", "height" : 186}
]
}';
SELECT JSON_VALID(@json); -- json 형식 만족하면 1, 아니면 0 반환
SELECT JSON_SEARCH(@json, 'one', '성시경'); -- 세 번째 파라미터 문자열 위치 반환, one은 처음 매치되는 하나만, all은 매치되는 모든 것
SELECT JSON_EXTRACT(@json, '$.userTBL[2].name'); -- 지정된 위치의 값 추출
SELECT JSON_INSERT(@json, '$userTBL[0].mDate', '2020-01-20'); -- 새로운 값 추가
SELECT JSON_REPLACE(@json, '$.userTBL[0].name', '홍길동'); -- 값 변경
SELECT JSON_REMOVE(@json, '$.userTBL[0]'); -- 지정된 항목 삭제
```



## 제약 조건

> 데이터의 무결성을 지키기 위한 제한된 조건

* PRIMARY KEY 제약 조건
  * 기본 키에 입력되는 값은 중복될 수 없음
  * NULL 값 입력될 수 없음
* FOREIGN KEY 제약 조건
  * 참조되는 테이블에 이미 데이터 존재해야 함
  * 참조되는 테이블의 열은 반드시 PRIMARY KEY거나 UNIQUE 제약 조건 있어야 함
* UNIQUE 제약 조건
  * 중복되지 않는 유일한 값 입력해야 함
  * PRIMARY KEY와 차이점은 NULL 값을 허용한다는 것
* CHECK 제약 조건
  * `CHECK (제약조건)` : 직접 조건을 지정하여 제약 조건에 위배되는 값은 입력이 안되도록 함
* DEFAULT 정의
  * 값을 입력하지 않았을 때 자동으로 입력되는 기본값 정의
* NULL 값 허용
  * NULL 값을 허용하려면 NULL, 허용하지 않으려면 NOT NULL 



## 뷰

> 일반 사용자 입장에서는 테이블과 동일하게 사용하는 개체



### 뷰의 장점

* 보안에 도움이 된다.
  * 중요한 정보를 제외한 데이터만 뷰로 생성
* 복잡한 쿼리를 단순화시켜줄 수 있다.
  * 자주 사용하는 쿼리를 뷰로 생성하여 접근



### 뷰 쿼리

``` sql
CREATE VIEW 뷰이름 AS ... -- 뷰 생성
ALTER VIEW 뷰이름 AS ... -- 뷰 수정
DROP VIEW 뷰이름; -- 뷰 삭제
```



















