# 인공지능을 위한 선형대수: Day1

> 네이버 부스트코스 강의 참고 https://www.boostcourse.org/ai251 



## Scalar, Vector, Matrix

### Scalar

하나의 숫자

### Vector

순서가 있는 숫자들의 배열

- Row vector : 가로 벡터
- Column vector : 세로 벡터 (기본)

++ 순서가 없는 배열은 set

### Matrix

행렬, 두 개의 축을 가지는 숫자들의 배열

가로(row, 행)와 세로(column, 열)을 가짐

행렬의 크기는 행(가로) × 열(세로)



## Matrix Notation (표기법)

- $A ∈ ℝ^{n×n}$

  Square matrix

  \#rows = #columns

- $A ∈ ℝ^{m×n}$

  Rectangular matrix

  \#rows ≠ #columns

- $A^T$

  Transpose of matrix

  전치행렬

- $A_{ij}$

  i : 행, j : 열

- $A_{i,:}$

  i번째 row의 모든 column

- $A_{:,i}$

  i번째 column의 모든 row

  

## Vector/Matrix Additions and Multiplications

- $C = A+B$

  $C_{ij} = A_{ij} + B_{ij}$

- $cA$

  상수배

- $C = AB$

  $C_{ij} = \sum_k A_{i,k}\ B_{k,j}$

  

## Properties

- Matrix multiplication is not commutative

  교환법칙 성립X

- Distributive

  분배법칙

  $A(B+C) = AB +AC$

- Associative

  결합법칙

  $A(BC) = (AB)C$

- Property of transpose

  $(AB)^T = B^TA^T$