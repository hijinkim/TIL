# 데코레이터



## 일급 시민

> 파이썬은 함수를 변수와 똑같은 방식으로 다루며 다양한 특징을 갖는다.
>
> * 이름을 가진다.
> * 다른 변수에 대입할 수 있다.
> * 인수로 전달할 수 있다.
> * 리턴할 수 있다.
> * 컬렉션에 저장할 수 있다.
>
> 일급 시민이란 모든 권리를 다 가지는 객체를 의미한다.
>
> 즉, 함수는 변수와 똑같이 취급한다.

``` python
def calc(op, a, b):
    op(a, b)

def add(a, b):
    print(a+b)
    
def multi(a, b):
    print(a*b)
    
calc(add, 1, 2)
calc(multi, 1, 2)
```



## 지역 함수

> 다른 함수 안에 정의되는 도우미 함수
>
> 길고 복잡한 동작을 수행하는 경우 일부 동작을 지역 함수로 정의

```python
def calcsum(n):
    def add(a, b):
        return a+b
    sum = 0
    for i in range(n+1):
        sum = add(sum, i)
    return sum

print(calcsum(10))
```



```python
def makeHello(message):
    def hello(name):
        print(message + ", " + name)
    return hello

enghello = makeHello("good morning")
enghello("Mr kim") #good morning, Mr kim
```

> makeHello 함수는 hello 함수를 생성하여 리턴
>
> enghello 변수에 대입되어 메모리에 계속 유지
>
> 지역 변수가 지속 기간이 긴 함수에 의해 계속 사용된다면 해석기는 이 변수를 없애지 않고 **클로저**라는 특수한 구조를 만들어 계속 유지



## 함수 데코레이터

> 기존 함수를 수정하지 않으면서 추가 기능을 구현할 때 사용

```python
def outer(func):
    def wrapper():
        print("-" * 20)
        func()
        print("-" * 20)
    return wrapper

@outer
def inner():
    print("결과 출력")
    
inner()
```



```python
def trace(func):
    def wrapper(*a, **b):
        r = func(*a, **b)
        print('{0}(a={1}, b={2}) -> {3}'.format(func.__name__, a, b, r))
        return r
    return wrapper

@trace
def get_max(*x):
    return max(x)

@trace
def get_min(**y):
    return min(y.values())

get_max(10, 20) #get_max(a=(10, 20), b={}) -> 20)
get_min(x = 10, y = 20, z = 30) #get_min(a=(), b={10, 20, 30}) -> 10
```



```python
def is_multiple(x):
    def real_decorator(func):
        def wrapper(a, b):
            r = func(a, b)
            if r % x == 0:
                print('{0}의 반환값은 {1}의 배수'.format(func.__name__, x))
            else:
                print('{0}의 반환값은 {1}의 배수 아님'.format(func.__name__, x))
            return r
        return wrapper
    return real_decorator

@is_multiple(3)
def add(a, b):
    return a+b

add(10, 20) #add의 반환값은 3의 배수
```



## 클래스 데코레이터

> 객체는 일종의 변수지만 괄호를 붙여 호출하면 클래스의 `__call__` 특수 메서드가 자동 호출
>
> 이를 이용하여 `__call__` 메서드에서 원래 함수를 호출하기 전이나 후에 추가 작업 가능



```python
class Outer:
    def __init__(self, func):
        self.func = func
    def __call__(self):
        print("-" * 20)
        self.func()
        print("-" * 20)

@Outer
def inner():
    print("결과 출력")
    
inner()
```



### 참고자료

* 파이썬 정복, 김상형, 한빛미디어

* https://blog.naver.com/612_44kk/221850415431









