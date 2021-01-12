# Python

> 귀도 반 로섬(Guido van Rossum)이 개발한 인터프리터 방식의 스크립트 언어



## 입출력

### 출력

* `print(출력 내용 [, sep = 구분자] [, end = 끝 문자])`



### 입력

* `변수 = input()`
* `변수 = int(input())`
* `변수1, 변수2 = map(int, input().split())`



## 변수

### 수치형

* 정수형
* 실수형
* 복소수형 : 실수부 + 허수부j



### 문자열

* 확장열
  * `\n` : 개행
  * `\t` : 탭
  * `\"` : 큰따옴표
  * ```\` ``` : 작은따옴표
  * `\\` : \문자
* 긴 문자열 : `"""`



### 진위형

* True
* False



### 컬렉션

* 리스트
* 튜플
* 딕셔너리
* 집합



## 연산자

### 산술 연산자

* `+` : 더하기
* `-` : 빼기
* `*` : 곱하기
* `/` : 나누기
* `**` : 거듭제곱
* `//` : 정수 나누기
* `%` : 나머지



## 조건문

### if , elif, else 문

```python
if 조건:
    명령
    
elif 조건:
    명령
    
else:
    명령
```



### 비교 연산자

* `==` : 같다
* `!=` : 같지 않다
* `<` , `>` : 크다, 작다
* `<=` , `>=` : 크거나 같다, 작거나 같다



### 논리 연산자

* `and` : 두 조건이 모두 참
* `or` : 두 조건 중 하나라도 참
* `not` : 주어진 조건이 아닐 때



## 반복문

### while 반복문

```python
while 조건:
    명령
```



### for 반복문

```python
for 제어변수 in 컬렉션:
    명령
    
for 제어변수 in range(시작, 끝, 증가값):
    명령
```



### break, continue

```python
for 제어변수 in 컬렉션:
    명령
    if 조건:
        break #반복문 탈출
    if 조건:
        continue #하나 건너뛰고 반복문 계속 실행
명령
```



## 함수

``` python
def 함수명(인수 목록):
    본체
    return 변수
```

* `pass` : 아무 동작도 하지 않음, 빈 코드 의미



### 인수

* `(*인수명)` : 가변 인수, 인수의 개수가 정해져 있지 않음, 튜플로 묶여서 전달, 인수 목록의 마지막에 와야 함, 2개 이상 사용 불가

* `(인수1 = 인수값, 인수 2 = 인수값)` : 키워드 인수, 이름 지정해서 순서 상관 없음, 위치 인수가 항상 먼저, 키워드 인수가 앞에 오면 뒤에 위치 인수 올 수 없음

* `(**인수명)` : 키워드 가변 인수, 여러 개의 키워드 인수를 전달하면 이름과 값의 쌍을 사전으로 만들어 전달

  ``` python
  def calcstep(**args):
      begin = args['begin']
      end = args['end']
      step = args['step']
      for num in range(begin, end + 1, step):
          ...
  
  calcstep(begin = 3, end = 5, step = 1)
  ```

* 인수의 기본값 : 기본값을 가지는 인수는 목록의 뒤쪽에 와야 함

  ``` python
  def calcstep(begin, end, step = 1):
      ...
  ```

  

### docstring

함수의 재활용성을 높이기 위해 자세한 함수 사용법이나 인수의 의미, 주의 사항을 남기는 공식적인 방법

`help(함수명)` 을 사용하여 docstring 출력 가능



## 문자열

### 슬라이스

* `[begin:end:step]` 
* 시작 위치 생략할 경우 0 적용
* 끝 위치 생략할 경우 문자열의 끝까지 추출
* 시작 위치는 포함, 끝 위치는 포함되지 않음, 끝 위치 직전의 문자까지만 추출



### 검색

* `find()` : 문자열 위치 조사, 없을 경우 -1 리턴
* `rfind()` : 뒤에서 검색 시작, 없을 경우 -1 리턴
* `index()` : 해당 문자 없을 경우 예외 발생
* `rindex()` : 뒤에서 검색
* `count()` : 문자의 개수 세기, 부문 문자열도 검색 가능



### 조사

* `단어 in 문자열` : 포함할 경우 True, 아니면 False 리턴
* `단어 not in 문자열` : 포함되어 있지 않은지 조사
* `startswith()` : 특정 문자열로 시작되는지 조사
* `endswith()` : 특정 문자열로 끝나는지 조사
* `isalpha()` : 알파벳인지
* `islower()`, `isupper()` : 소문자, 대문자인지
* `isspace()` : 공백인지
* `isalnum()` : 알파벳 또는 숫자인지
* `isdecimal()` , `isdigit()` , `isnumeric()` : 숫자인지
* `isdentifier()` : 명칭으로 쓸 수 있는 문자로만 구성되어 있는지
* `isprintable()` : 인쇄 가능한 문자로만 구성되어 있는지



### 변경

* `lower()` : 소문자로
* `upper()` : 대문자로
* `swapcase()` : 소문자는 대문자로, 대문자는 소문자로
* `capitalize()` : 문장의 첫 글자만 대문자로
* `title()` : 모든 단어의 첫 글자를 대문자로
* `strip()` : 양쪽 공백 제거
* `lstrip()` , `rstrip()` : 왼쪽 공백 제거, 오른쪽 공백 제거



### 분할

* `split()` : 구분자를 기준으로 문자열 분할, 인수 없을 경우 공백 기준
* `splitlines()` : 개행 문자나 파일 구분자, 그룹 구분자 등을 기준으로 분할
* `join()` : 문자열의 각 문자 사이에 다른 문자열 끼워 넣기



### 대체

* `replace()` : 첫 번째 인수로 검색할 문자열, 두 번째 인수로 바꿀 문자열 지정, 세 번째 인수로 바꿀 개수 지정
* `ljust()` : 좌측 정렬, 인수로 폭 지정
* `rjust()` : 우측 정렬, 인수로 폭 지정
* `center()` : 가운데 정렬



### 포맷팅

```python
year = 2021
print("올해는 " + str(year) + "년")
print("올해는 ", year, "년")
```

| 표식 |   설명    |
| :--: | :-------: |
|  %d  |   정수    |
|  %f  |   실수    |
|  %s  |  문자열   |
|  %c  | 문자 하나 |
|  %h  |  16진수   |
|  %o  |   8진수   |
|  %%  |  % 문자   |

```python
year = 2021
month = 1
day = 11
print("오늘은 %d년 %d월 %d일", %(year, month, day))
```

* `[-]폭[.유효자리수]서식`
  * `-` 지정시 왼쪽 정렬
  * `.` 기호로 소수점 이하 얼마까지 표시할 것인지 지정



### 신형 포맷팅

* `print("이름: {}, 나이: {}, 키: {}".format(name, age, height))`
* `print("이름: {1}, 나이: {2}, 키: {0}".format(height, name, age))`

* `print("이름: {name}, 나이: {age}, 키: {height}.format(name = "한결", age = 20, height = 160))`
* ``print("이름: {0:10s}, 나이: {1:5d}, 키: {2:7.2f}".format(name, age, height)`
* `print("이름: {0:^10s}, 나이: {1:>5d}, 키: {2:<7.2f}".format(name, age, height))` (< 왼쪽 정렬, > 오른쪽 정렬, ^ 가운데 정렬)



## 리스트

* `리스트명[범위1:범위2] = []` : 해당 범위의 요소 제거
* `리스트1 + 리스트2` : 두 리스트 연결
* `리스트 * 정수` : 요소를 정수 번 반복



### 리스트 Comprehension

* `[수식 for 변수 in  리스트 if 조건]`
  * `[n * 2 for n in rane(1, 11)]` #[2, 4, 6, 8, ... , 18, 20]
  * `[n * n for n in range(1, 11) if n % 3 == 0]` #[9, 36, 81]



### 삽입

* `append()` : 인수로 전달한 요소를 리스트 끝에 추가
* `insert()` : 삽입할 위치와 요소값 전달받아 리스트 중간에 삽입
* `extend()` : 호출한 리스트에 인자로 주어진 리스트 합침 (list1 = list1 + list2와 같음)



### 삭제

* `remove()` : 인수로 전달받은 요소값을 찾아 삭제, 해당 값 없으면 예외 발생, 2개 이상이면 처음 발견한 요소만 삭제
* `del 리스트[인덱스]` : 요소 하나 삭제
* `clear()` : 모든 요소 삭제
* `pop()` : 삭제한 요소 리턴, 인수 없으면 마지막 요소 삭제하고 리턴



### 검색

* `index()` : 특정 요소의 위치 찾기, 발견되지 않으면 예외
* `count()` : 특정 요소값의 개수 조사
* `len()` : 리스트의 길이
* `max()` : 리스트의 최대값
* `min()` : 리스트의 최소값
* `in` , `not in` : 요소가 있는지 검사



### 정렬

* `sort()` : 리스트 정렬, 오름차순 정렬
  * `sort(reverse = True)` : 내림차순 정렬
  * `sort(key = str.lower)` : 소문자로 바꾼 후 비교
* `reverse()` : 요소의 순서를 반대로 뒤집기
* `sorted()` : 정렬된 새로운 리스트 만들어서 리턴



## 튜플

> 튜플을 사용하는 이유는 리스트에 비해 속도가 빠르고 편집할 수 없어서 안정적이기 때문이다.

### unpacking

```python
tu = "가", "나", "다"
a, b, c = tu

#a = "가"
#b = "나"
#c = "다"
```



### 두 개 이상의 값 반환

```python
import time
def gettime():
    now = time.localtime()
    return now.tm_hour, now.tm_min #두 값이 튜플로 묶여 반환

result = gettime()
print('지금은 %d시 %d분 입니다' %(result[0], result[1]))
```



## 딕셔너리

* `get()` : 키가 없으면 None 리턴, 두 번째 인수로 대신 돌려줄 디폴트값 지정 가능
* `키 in 사전` : 키가 있으면 True, 없으면 False 리턴

* `사전[키] = 값` : 키가 이미 존재할 경우 기존 값 변경, 없는 키일 경우 새로운 키와 값 쌍이 추가
* `del[키]` : 해당 키를 찾아 값과 함께 삭제, 키가 없으면 예외 발생
* `keys()` : 키 리스트 리턴
* `values()` : 값 리스트 리턴
* `items()` : 키와 값을 튜플로 묶은 객체 리턴
* `update()` : 인수로 전달한 사전이 호출 사전에 병합, 중복되는 키 있으면 병합되는 키 값 적용



## 집합

> 집합은 중복을 허용하지 않음

* `set()`
* `add()` : 원소 추가
* `remove()` : 원소 제거
* `update()` : 집합끼리 결합, 합집합
* `집합1 & 집합2` , `집합1.intersection(집합2)` : 교집합
* `집합1 | 집합2` , `집합1.union(집합2)` : 합집합
* `집합1 - 집합2` , `집합1.difference(집합2)` : 차집합
* `집합1 ^ 집합2` , `집합1.symmetric_difference(집합2)` : 배타적 차집합
* `<= ` , `issubset()` : 부분집합인지 조사
* `>=` , `issuperset` : 포함집합인지 조사



## 컬렉션 관리

### enumerate

> 순서값과 요소값을 튜플로 묶은 컬렉션을 리턴
>
> 두 번째 인수로 시작값 지정 가능

```python
score = [10, 20, 30, 40, 50]
for no, s in enumerate(score, 1):
    print(str(no) + '번 학생의 성적 :', s)
```



### zip

> 여러 개의 컬렉션을 합쳐 하나로 만든다
>
> 두 리스트의 대응되는 요소끼리 짝을 지어 튜플 리스트 생성

```python
yoil = ['월', '화', '수', '목', '금']
food = ['갈비탕', '순대국', '칼국수']
menu = zip(yoil, food)
dict(zip(yoil, food)) #yoil이 키, food가 값인 딕셔너리
```



### any, all

* `any` : 리스트에 참인 요소가 하나라도 있는지, 빈 리스트인 경우 거짓
* `all` : 리스트의 모든 요소가 참인지, 빈 리스트인 경우 참



### filter

> 리스트의 요소 중 조건에 맞는 것만 골라내는 것
>
> 첫 번째 인수는 조건 지정, 두 번째 인수는 대상 리스트

```python
def flunk(s):
    return s < 60

score = [10, 20, 50, 60, 70]
for s in filter(flunk, score):
    print(s)
```



### map

> 모든 요소에 대해 변환 함수를 호출하여 새 요소값으로 구성된 리스트 생성
>
> filter와 인수 구조 동일

```python
def total(s, b):
    return s + b

score = [10, 20, 30, 40, 50]
bonus = [5, 4, 3, 2, 1]
for s in map(total, score, bonus):
    print(s)
```



### 람다 함수

> `lambda 인수 : 식`
>
> 이름이 없고 입력과 출력만으로 함수를 정의
>
> 인수는 여러 개 가능, 인수로부터 계산한 식 리턴

```python
score = [10, 20, 30, 40, 50]
for s in map(lambda x:x / 2, score):
	print(s)
```



### 리스트 사본

* `list2 = list1.copy()`

* `list2 = list[:]`

* `list2 = copy.deepcopy(list1)`

  ```python
  list0 = ['a', 'b']
  list1 = [list0, 1, 2]
  list2 = list1.copy()
  
  list2 = [0][1] = 'c'
  
  #list1 = [['a', 'c'], 1, 2]
  #list2 = [['a', 'c'], 1, 2]
  #list1과 list2가 내부의 list0을 공유
  #완전한 사본을 만들기 위해서는 deepcopy 사용
  ```



### is

 두 변수가 같은 객체를 가리키고 있는지

 컬렉션에 대한 대입은 별명을 하나 더 만드는 것과 같음, 완전한 사본을 만드려면 copy 메서드로 메모리 복사

 정수는 대입에 의해 일시적으로 같은 객체를 가리킬 수 있지만 다른 값을 대입하면 참조가 변경되어 즉시 분리



## 표준 모듈

### math 모듈

#### math 모듈에 정의된 상수

* `pi` : 원주율 상수
* `tau` : 원주율의 2배 되는 상수
* `e` : 자연 대수 상수
* `inf` : 무한대 값
* `nan` : 숫자가 아닌 값



#### math 모듈 함수

* `sqrt(x)` : x의 제곱근
* `pow(x, y)` : x의 y승
* `hypot(x, y)` : x제곱 + y제곱의 제곱근
* `factorial(x)` : x의 계승
* `sin(x)` , `cos(x)` , `tan(x)` : 삼각함수
* `asin(x)` , `acos(x)` , `atan(x)` , `atan2(y, x)` : 역삼각함수
* `sinh(x)`, `cosh(x)` , `tanh(x)` : 쌍곡선 삼각함수
* `asinh(x)` , `acosh(x)` , `atanh(x)` : 쌍곡선 역삼각함수
* `degrees(x)` : 라디안 값을 각도로
* `radians(x)` : 각도를 라디안 값으로
* `ceil(x)` : 수직선 오른쪽의 올림 값
* `floor(x)` : 수직선 왼쪽의 내림값
* `fabs(x)` : x의 절대값
* `trunc(x)` : x의 소수점 이하 버림
* `log(x, base)` : base에 대한 x의 로그
* `log10(x)` : 10의 로그
* `gcd(a, b)` : a, b의 최대공약수



### statistics 모듈

#### statistics 모듈 함수

* `mean` : 평균
* `harmonic_mean` : 조화평균
* `median` : 중앙값, 짝수인 경우 보간 값
* `median_low` : 중앙값, 집합 내 낮은 값
* `median_high` : 중앙값, 집합 내 높은 값
* `median_grouped` : 그룹 연속 중앙값
* `mode` : 최빈값
* `pstdev` : 모표준편차
* `stdev` : 표준편차
* `variance` : 분산



### time 모듈

#### time 모듈 함수

* `time` : 에폭시간, 유닉스 시간
* `ctime` : 문자열 형태의 날짜, 시간
* `localtime` : 현지 시간
* `gmtime` : 세계 표준 시간
* `sleep(x)` : x초 대기 후 실행



### calendar 모듈

#### calendar 모듈 함수

* `calendar` : 인수로 받은 년도의 달력 객체 리턴
* `month` : 인수로 년도와 달을 받아 해당 월의 달력 객체 리턴
* `prcal` : 인수로 받은 년도의 달력 직접 출력
* `prmonth` : 인수로 년도와 달을 받아 해당 월의 달력 직접 출력
* `weekday` : 특정 날짜가 무슨 요일인지



### random 모듈

#### random 모듈 함수

* `random` : 0에서 1 미만의 실수 하나 생성
* `randint(begin, end)` : begin ~ end 사이의 정수 난수 중 하나, end도 범위 포함
* `uniform` : 실수 난수 생성
* `choice` : 리스트에서 임의의 요소 하나 리턴
* `shuffle` : 리스트의 요소 무작위로 섞음
* `sample` : 리스트 항목 중 n개를 무작위로 뽑아 새로운 리스트 생성



### sys 모듈

#### sys 모듈 함수

* `version `: 버전
* `platform` : 플랫폼
* `byteorder` : 바이트 순서
* `path` : 모듈 경로
* `argv` : 명령행 인수 값 읽기
* `exit` : 프로그램 강제 종료



## 예외 처리

```python
try:
    실행할 명령
except 예외 as 변수:
    오류 처리문
else:
    예외가 발생하지 않을 때의 처리
```



### 예외의 종류

* `NameError` : 명칭이 발견되지 않음, 초기화되지 않은 변수 사용시 발생
* `ValueError` : 타입은 맞지만 값의 형식이 잘못됨
* `ZeroDivisionError` : 0으로 나눈 경우
* `IndexError` : 첨자가 범위를 벗어남
* `TypeError` : 타입이 맞지 않음



### raise

> 고의적으로 예외 발생시킴

```python
def calcsum(n): #1부터 n까지의 합 구하는 함수
    if n < 0:
        raise ValueError #return -1로도 표현 가능
    ...
    
    
try:
    calcsum(-5)
except ValueError:
    오류메시지
```



## 자원정리

### finally

> 예외 발생 여부와 상관없이 반드시 실행해야 할 명령 지정

```python
try:
    실행할 명령
finally:
    예외 발생 여부와 상관없이 실행할 명령
```



### assert

> 프로그램의 현재 상태가 맞는지 확인
>
> 이상이 발생하는 즉시 이를 확인하여 알려주는 역할
>
> 디버깅할 때 확인용

```python
#assert 조건, 메시지
assert score <= 100, '점수는 100 이하여야 합니다'
```







