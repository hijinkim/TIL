# `if __name__ == '__main__':`

### Example 1

#### a.py

```python
def func():
    print('func A')
    
if __name__ == '__main__':
    print('main A')
else:
    print('import A')
```
#### b.py

```python
import a

a.func()

if __name__ == '__main__':
    print('main B')
else:
    print('import B')
```
#### b.py 실행결과

```
import A
func A
main B
```

---

### Example 2

#### a.py

```python
def add(a, b):
    return a + b

print(add(0, 0))
```

#### b.py

```python
import a

print(a.add(5, 5))
```

#### b.py 실행결과

```
0
10
```

:arrow_forward: a.add(5, 5)의 결과만 출력되는 것을 원했지만 a.py의 print(add(0, 0))이 함께 실행 되었다.

---

### Example 2 수정

#### a.py

```python
def add(a, b):
    return a + b

if __name__ == '__main__':
    print(add(0,0))
```

#### b.py 실행결과

```
10
```

---

`__name__` 은 현재 모듈의 이름을 담고 있는 내장 변수이다.

모듈이 직접 실행되는 경우 `__name__` 은 `'__main__'` 값이 할당된다.

모듈을 import 하여 사용하는 경우 `__name__` 은 모듈 이름이 할당되게 된다.

즉, import 되어 실행되는 경우에는 `if __name__ == '__main__'` 안의 내용이 실행되지 않는다.