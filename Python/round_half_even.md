# 파이썬 반올림

### round()

일반적으로 0.5를 반올림하면 1이 된다고 생각한다.

하지만 파이썬에서 `round(0.5)` 를 실행하면 0이 출력된다.

**ROUND_HALF_EVEN** 방식을 사용하기 때문이다.

우리가 사용하는 일반적인 반올림은 **ROUND_HALF_UP** 방식이다.



### ROUND_HALF_EVEN?

ROUND_HALF_EVEN 방식은 중간값에서 반올림하는 경우 짝수 쪽에 가깝도록 반올림하는 방식이다.

즉, 0.5는 우리가 아는 방식으로 반올림하면 1, 홀수가 되므로 버림 연산을 한다.

1.5는 2, 즉 짝수가 되므로 올림 연산을 한다.

그래서 `round(0.5)` 는 0, `round(1.5)` 는 2가 된다.



이런 방식을 사용하는 이유는 ROUND_HALF_UP 방식이 대칭적이지 않다는 문제가 있기 때문이다.

ROUND_HALF_UP 방식으로 계산을 하게 되면 항상 큰 쪽으로 계산되기 때문에 전체 값이 상승하게 된다.

예를 들어 0.1~1.9까지 반올림을 한다고 했을 때 ROUND_HALF_UP 방식을 사용하면 평균이 약 1.1이 된다.

하지만 ROUND_HALF_EVEN  방식을 사용하면 평균이 1.0이 된다.



### ROUND_HALF_UP 방식 사용하기

* int() 사용 (실수에 대해 int 함수 호출하면 소수점 이하 버림)

  ```python
  int(0.5 + 0.5) #1
  int(1.6 + 0.5) #2
  int(1.3 + 0.5) #1
  ```

* decimal 클래스 사용1

  ```python
  context = decimal.getcontext()
  context.rounding = decimal.ROUND_HALF_UP
  print(round(decimal.Decimal('0.5'), 0))
  ```

  * `round(decimal.Decimal('0.5'), 0)` : 반올림할 수, 반올림하고 남는 유효 자리수 지정

    (`round(decimal.Decimal('0.555'), 2)` 실행하면 0.56)

* decimal 클래스 사용2

  ```python
  x = decimal.Decimal('2.5').quantize(decimal.Decimal('0'), rounding=decimal.ROUND_HALF_UP)
  print(x)
  ```

  * `.quantize(decimal.Decimal('0'), rounding=decimal.ROUND_HALF_UP)` : 표현 형식 지정, 반올림 방식 지정

    (`decimal.Decimal('2.555').quantize(decimal.Decimal('0.00'), rounding=decimal.ROUND_HALF_UP)` 실행하면 2.56)

* math 모듈 사용 (floor(), 버림 함수 사용)

  ``` python
  math.floor(1.5 + 0.5) #2
  math.floor(1.6 + 0.5) #2
  math.floor(1.3 + 0.5) #1
  ```

  



















