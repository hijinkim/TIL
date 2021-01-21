#### :book: 이것이 MariaDB다, 우재남, 한빛미디어 참고



# SQL_DDL

> DDL (Data Define Language)
>
> 데이터베이스 구조, 데이터 형식, 접근 방식 등 데이터베이스를 구축하거나 수정할 목적으로 사용하는 언어



## CREATE

```sql
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] 테이블이름 (create_definition ... ) [table_options] ... [partition_options]

create_definition: 
	{col_name column_definition | index_definition | period_definition | CHECK (expr)}

column_definition:
	data_type
		[NOT NULL | NULL] [DEFAULT default_value | (expression)]
		[AUTO_INCREMENT] [UNIQUE [KEY] | [PRIMARY] KEY]
		[INVISIBLE] [{WITH|WITHOUT} SYSTEM VERSIONING]
		[COMMENT 'string']
		[COLUMN_FORMAT {FIXED|DYNAMIC|DEFAULT}]
		[reference_definition]
	|data_type [GENERATED ALWAYS] AS {{ROW {START|END}} | (expression) [VIRTUAL|PERSISTENT]}}
	[UNIQUE [KEY]] [COMMENT 'string']
```

* `NULL | NOT NULL` : 디폴트는 NULL, 빈 값 허용 | 반드시 값 입력

* `AUTO_INCREMENT` : 반드시 PRIMARY KEY 혹은 UNIQUE 지정

* `CONSTRAINT PRIMARY KEY 기본키이름 (기본키로 지정할 열이름)` : 기본 키 이름 지정, CONSTRAINT 생략 가능

* `CONSTRAINT 외래키이름(열 이름) REFERENCES 참조할테이블명(열 이름)` 

  

## ALTER

```sql
ALTER [ONLINE] [IGNORE] TABLE 테이블이름
	[WAIT n | NOWAIT]
	alter_specification [, alter_specification]
```

* `ADD 열이름` : 열 추가
  * FIRST : 제일 앞에 열 추가
  * AFTER 열 이름 : 열 이름 다음에 추가
* `DROP COLUMN 열이름` : 제약 조건이 걸린 경우 제약조건 먼저 삭제
* `CHANGE COLUMN 열이름 변경할이름 데이터형식` : 열 이름 및 데이터 형식 변경
* `DROP 제약 조건` : 열의 제약 조건 삭제
* `ADD 제약 조건` : 열의 제약 조건 추가
* `ON [DELETE | UPDATE] CASCADE` : 연관된 행도 함께 변경



## DROP

```sql
DROP TABLE 테이블이름;
```

* 외래 키 제약 조건의 기준 테이블은 삭제 불가
  * 외래 키가 생성된 외래 키 테이블 먼저 삭제 해야 함
* `DROP TABLE 테이블1, 테이블2, 테이블3 ...; ` : 여러 개의 테이블 삭제 가능