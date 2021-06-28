# HSV

색상 공간

BGR/RGB 패턴으로는 인간이 인지하는 영역의 색상을 구별하기 어렵고 복잡함

HSV 색상 공간을 활용하면 간편하고 빠르게 특정 색상 검출 및 분리 가능

### Hue

빨간색, 파란색 등으로 인식되는 색상 중 하나 또는 둘의 조합과 유사한 것처럼 보이는 시각적 감각의 속성

0˚ ~ 360˚ 범위로 표현

openCV에서는 0 ~ 179 범위 ( 1 Byte를 넘기 때문에 불필요한 메모리 사용을 줄이기 위함)



### Saturation

이미지의 색상 깊이, 색상이 얼마나 순수한 색인지 의미

0 ~ 100%의 비율로 표현

0에 가까울수록 무채색, 100에 가까울수록 순수한 색

openCV에서는 0 ~ 255



### Value

색의 밝고 어두운 정도, 높을수록 색상이 밝고 낮을수록 색상이 어두워짐

0 ~ 100%의 비율로 표현

0에 가까울수록 검은색, 100에 가까울수록 가장 맑은색

openCV에서는 0 ~ 255



## Code

```python
src = cv2.imread('Image/ray.jpg', cv2.IMREAD_COLOR)
hsv = cv2.cvtColor(src, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv)

cv2.imshow('h', h)
cv2.imshow('s', s)
cv2.imshow('v', v)
cv2.waitKey()
cv2.destroyAllWindows()
```



## Detailed Code

```python
hsv = cv2.cvtColor(src, cv2.COLOR_BGR2HSV)
```

색상 공간 변환 함수



```python
h, s, v = cv2.split(hsv)
```

채널 분리 함수



## Code2

```python
src = cv2.imread('Image/ray.jpg', cv2.IMREAD_COLOR)
hsv = cv2.cvtColor(src, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv)

h = cv2.inRange(h, 8, 20)
orange = cv2.bitwise_and(hsv, hsv, mask=h)
orange = cv2.cvtColor(orange, cv2.COLOR_HSV2BGR)

cv2.imshow('orange', orange)
cv2.waitKey()
cv2.destroyAllWindows()
```



## Detailed Code2

### 배열 요소 범위 설정 함수

```python
h = cv2.inRange(h, lowerb, upperb)
```

`lowerb` 낮은 범위

`upperb` 높은 범위

++ 주황색은 8 ~ 20 범위



### 마스크 덧씌우기

```python
orange = cv2.bitwise_and(src1, src2, mask)
```

마스크를 사용해 이미지 위에 덧씌워 해당 부분만 출력

픽셀의 이진값이 동일한 영역만 AND 연산하여 반환









