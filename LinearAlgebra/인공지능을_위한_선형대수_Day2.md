# 인공지능을 위한 선형대수: Day1

> 네이버 부스트코스 강의 참고 https://www.boostcourse.org/ai251 



## 선형방정식

$$
a_1x_1+a_2x_2+...+a_nx_n=b
$$

$$
\mathbf{a}^\mathbf{T}\mathbf{x} = b
$$

$$
\mathbf{a} = \begin{bmatrix} a_1 \\ a_2 \\ ... \\ a_n \end{bmatrix}$ $\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ ... \\ x_n \end{bmatrix}
$$



## 선형시스템

선형방정식들의 집합, 연립방정식

### 선형시스템 예시

$$
60x_1+5.5x_2+x_3=66
$$

$$
65x_1+5.0x_2+0x_3=74
$$

$$
55x_1+6.0x_2+x_3=78
$$

$$
\begin{bmatrix} 60 & 5.5 & 1 \\ 65 & 5.0 & 0 \\ 55 & 6.0 & 1 \end{bmatrix} \ \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} \ = \begin{bmatrix} 66 \\ 74 \\ 78 \end{bmatrix}
$$



## 항등행렬

정사각 행렬
$$
I_3 = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$

$$
\forall \mathbf{x} \in \mathbb{R}^n, \ I_n\mathbf{x} = \mathbf{x}
$$

 ( 어떤 벡터와 곱해져도 그 벡터 자기 자신이 됨)

## 역행렬

정사각 행렬에서만 존재
$$
A^{-1}A = AA^{-1}=I_n
$$

$$
A^{-1} = {1 \over ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}
$$



## 역행렬로 선형시스템 풀기

$$
A\mathbf{x} = \mathbf{b}
$$

$$
A^{-1}A\mathbf{x} = A^{-1}\mathbf{b}
$$

$$
I_n\mathbf{x} = A^{-1}\mathbf{b}
$$

$$
\mathbf{x} = A^{-1}\mathbf{b}
$$



## 역행렬이 존재하지 않을 때

$$
A^{-1} = {1 \over ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}
$$

에서 
$$
ad-bc
$$
(판별식, det A)가 0일 때 역행렬 존재하지 않음

⇒ 
$$
ad = bc
$$
⇒
$$
a:b = c:d
$$
역행렬이 존재하지 않으면 해가 없거나 무수히 많음

만약 A가 직사각 행렬일 경우 ( $A \in \mathbb{R}^{m×n}$ )

- $$
  m < n
  $$

  해가 무수히 많음 (under-determined system)

- $$
  m > n
  $$

  해가 존재하지 않음 (over-determined system)

⇒ 가장 근사하게 만족하는 경우로 문제를 풀게 됨







