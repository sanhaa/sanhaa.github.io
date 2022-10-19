---
layout: post
title: Numpy | 선형대수학 기초, 행렬 곱 연산(dot(), *, @)
description: >
  선형대수학 기초와 numpy 함수, 행렬의 곱 연산 차이
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}


~~~python
import numpy as np
~~~

## 행렬
n차원 행렬 만들기  
~~~python
A = np.array([[1, 2, 3],
            [4, 5, 6]])
~~~
A는 (2, 3)의 `matrix`, `행렬` 


## 행렬 연산
~~~python
A = np.array([[1, 2, 3],
            [4, 5, 6]])

B = np.array([[2, 2, 2],
            [3, 3, 3]])
~~~

**행렬끼리 더하기**  
~~~python
print(A+A)
'''
[[ 2  4  6]
 [ 8 10 12]]
'''
print(A+B)
'''
[[3 4 5]
 [7 8 9]]
 '''
~~~

**행렬끼리 빼기**
~~~python
print(A-A)
'''
[[0 0 0]
 [0 0 0]]
'''
print(A-B)
'''
[[-1  0  1]
 [ 1  2  3]]
 '''
~~~

## 중요한 행렬의 곱셈 (* vs. @ vs. dot())

~~행렬의 곱셈은 어렵기 때문에, 자세히 살펴봐야 한다.~~

아래 코드 실행 결과를 예상해보자.

~~~python
X = np.array([[1, 2],
            [3, 4]])
Y = np.array([[1, 1],
            [2, 2]])

print(X*Y) # 1
print(X.dot(Y)) # 2
print(X@Y) # 3
~~~

### 1. * 연산
numpy 연산자 *는 matrix의 같은 위치에 있는 원소끼리 곱한다.

~~~python
print(X*Y) # 1
'''
[[1 2]
 [6 8]]
'''
~~~

- numpy * operator: `X*Y`
- element-wise
- 연산하려는 matrix shape이 동일해야 한다. `(n, m) * (n, m) = (n, m)`
- np.multiply(X, Y)를 연산자 `*`로 축약해서 사용함

### 2. np.dot() 연산
[numpy.dot](https://numpy.org/doc/stable/reference/generated/numpy.dot.html#numpy.dot): 두 vector의 내적을 계산하는 함수

*피연산자의 array 차원에 따라 계산 방법이 조금씩 다르니 아래의 설명 혹은 공식 문서를 참고*

~~~python
print(X.dot(Y)) # 2
'''
[[ 5  5]
 [11 11]]
'''
~~~

- numpy.dot: `X.dot(Y)`
- X, Y가 모두 1차원 array(vector) -> 벡터의 내적 연산
- X, Y가 모두 2차원 array(행렬) -> 행렬 곱 연산 (그러나 `matmul`이나 `X@Y` 사용을 권장)
- X, Y 둘 중에 하나가 scalar 값이라면 -> 곱셈연산 (그러나 `np.multiply(X, Y)` 혹은 `X*Y` 사용을 권장)
- X가 N차원 array, Y가 1차원 array(vector) -> X의 마지막 axis 기준으로 sum 연산
- X, Y가 모두 2차원 이상의 array(텐서)이라면 -> X의 마지막 축, Y의 마지막에서 두번째 축의 기준으로 sum 연산
    > dot(a, b)[i,j,k,m] = sum(a[i,j,:] * b[k,:,m])

~~~python
# N-D array, 1-D array dot 연산 예시
a = np.arange(8).reshape(2, 4); 
'''
array([[0, 1, 2, 3],
       [4, 5, 6, 7]])
'''
b = [10, 10, 10, 10]
a.dot(b)
### >>> array([ 60, 220])
~~~

~~~python
# N-D array, 1-D array dot 연산 예시
c = np.arange(16).reshape(2, 2, 4)
'''
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7]],

       [[ 8,  9, 10, 11],
        [12, 13, 14, 15]]])
'''
d = [1, 1, 1, 1]
c.dot(d)
### >>> array([[ 6, 22],
### >>>    [38, 54]])
~~~


### 3. matmul() 과 @  
 [numpy.matmul](https://numpy.org/doc/stable/reference/generated/numpy.matmul.html): 다차원 array의 곱셈을 수행한다.

~~~python
X = np.arange(2*3*4).reshape((2, 3, 4))
'''
[[[ 0  1  2  3]
  [ 4  5  6  7]
  [ 8  9 10 11]]

 [[12 13 14 15]
  [16 17 18 19]
  [20 21 22 23]]]
'''
Y = np.arange(2*3*4).reshape((2, 4, 3))
'''
[[[ 0  1  2]
  [ 3  4  5]
  [ 6  7  8]
  [ 9 10 11]]

 [[12 13 14]
  [15 16 17]
  [18 19 20]
  [21 22 23]]]
'''

print(np.matmul(X, y).shape)
### >>> (2, 3, 3)

# 아래 두 연산 동일
print(X@Y) # 3
print(np.matmul(X, Y)) 

'''
[[[  42   48   54]
  [ 114  136  158]
  [ 186  224  262]]

 [[ 906  960 1014]
  [1170 1240 1310]
  [1434 1520 1606]]]
'''
~~~

> The @ operator can be used as a shorthand for np.matmul on ndarrays.

- `np.matmul()` 연산을 `@` 연산자로 줄여서 나타낼 수 있다.
- X의 마지막 차원 = Y의 마지막에서 두번째 차원(second-to-last)이 같아야 함
    > (n, k) (k, m) = (n, m)과 똑같다. k로 같아야 함
- 결국 matmul은 마지막 (n, m) 2차원을 박스로 보고, 그 박스가 몇 개 (몇 차원)인지

## 그래서 dot과 matmul

- `dot()`은 N-D array와 scalar끼리 연산 가능 (matmul은 피연산자가 모두 N-D array)
- 2차원 행렬: `dot()`과 `matmul()`의 연산 결과 동일
- 3차원 이상 array: `dot()`과 `matmul()` 연산 결과가 **다름**

~~~python
a = np.ones([9, 5, 7, 4])
c = np.ones([9, 5, 4, 3])

np.dot(a, c).shape
### >>> (9, 5, 7, 9, 5, 3)
np.matmul(a, c).shape
### >>> (9, 5, 7, 3)

# 앞에 차원 제외하고 뒤에 2차원 행렬 곱처럼 (7, 4) x (4, 3) = (7, 3)으로 나왔다고 생각
~~~


## 정리
- 행렬(2차원) 곱에는 np.dot()과 matmul()의 연산 결과가 같다.
- 그러나 고차원 배열 혹은 텐서의 곱셈에서는 계산 결과가 전혀 다르다.
- 텐서에 대해서는 나중에 정리해야지

<br>

---

## Reference
- [블로그: python 행렬 곱연산 @](https://cyber0946.tistory.com/64) 
- [위키피디아: 행렬의 곱셈 원리](https://ko.wikipedia.org/wiki/%ED%96%89%EB%A0%AC_%EA%B3%B1%EC%85%88)
- [블로그: dot vs. matmul 계산 원리](https://blog.naver.com/cjh226/221356884894) 