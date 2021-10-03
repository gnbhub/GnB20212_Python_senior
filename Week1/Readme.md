# 1주차 Numpy, Pandas
## NumPy?
![image](https://user-images.githubusercontent.com/79446573/135745988-adb223aa-401c-44c2-a33d-7859e27298f6.png)
<br>공식 홈페이지 : http://www.numpy.org/
 - Numarray와 Numeric이라는 오래된 Python 패키지를 계승해서 나온 수학 및 과학 연산을 위한 파이썬 패키지
 - Numpy 내부는 상당부분 C나 포트란으로 작성되어 실행 속도도 꽤 빠른편이다. 
 - 기본적으로 array라는 자료를 생성하고 이를 바탕으로 색인, 처리, 연산 등을 하는 기능을 수행한다.
 - 사용될 때 주로 Scipy, Pandas, matplotlib 등 다른 Python 패키지와 함께 쓰이는 경우가 많다.
 - 파이썬으로 수치해석, 통계 관련 기능을 구현한다고 할 때 Numpy는 가장 기본이 되는 모듈이다.

### 모듈 메소드
#### 모듈 불러오기
```python
import numpy
```
주로 편의를 위해 numpy를 np로 줄여 import한다.
```python
import numpy as np
```
#### 넘파이 array 선언
```python
arr1 = np.array([2, 3, 5, 8, 10])
```
 - numpy.ndarray 타입의 배열을 직접 선언한다.
```python
arr2 = np.full(2, 5)  #[5 5]
```
 - np.full(size, value) : size 만큼 모두 동일한 value로 배열을 선언한다.
```python
arr3 = np.zeros(6, dtype = int) # [0 0 0 0 0 0]
```
 - np.zeros(size, dtype) : size만큼 원하는 dtype으로 0을 채워 배열을 선언한다.
 
<br>※python은 value 자체로 데이터 타입을 구분할 수 없다. 따라서 어떤 dtype인지 선언해야 한다.
```python
arr4 = np.ones(6, type = int) # [1 1 1 1 1 1]
```
 - np.ones(size, dtype) : size만큼 원하는 dtype으로 1을 채워 배열을 선언한다.
```python
arr5 = np.random.random(5) #[0.87603185 0.02095331 0.69657018 0.6549163 0.74435118]
```
 - np.random.random(size, size, ...) : NumPy의 random 모듈 내의 random 메소드를 이용하여 난수를 채워 배열을 선언하는데, size를 병렬로 쓰는 만큼 차원이 늘어난다.
#### 연속된 값을 가진 numpy array 생성
arrange메소드를 사용하면 연속된 값을 가진 numpy array를 생성할 수 있다.
```python
arr6 = np.arange(5) # [0 1 2 3 4]
arr7 = np.arange(5,7) # [5 6]
arr8 = np.arange(5, 10, 2) # [5 7 9]
```
 - 인자가 1개일 경우 `np.arange(n)` : 0부터 n - 1 까지의 값이 담긴 배열 선언
 - 인자가 2개일 경우 `np.arange(n, m)` : n부터 m-1까지 값이 담긴 배열 선언
 - 인자가 3개일 경우 `np.aragne(n, m, s) : n부터 m-1의 값 중에서 간격이 s인 값이 담긴 배열 선언
#### 인덱싱
리스트와는 달리 원하는 index의 값을 여러개 선택하여 추출할 수 있다.
```python
arr = np.array([2, 5, 6, 7, 9, 11])
arr[0] #2
arr[[0, 3, 5]] # [2 7 9]
```
[] 안에 []이 있는 모양이다. 즉, index는 dtype이 int인 ndarry를 통해서도 가능하다.
```python
arr1 = np.array([2, 5, 6, 7, 9, 11])
arr2 = np.array([1, 2, 4])
arr1[arr2] # [5 6 9]
```
#### 슬라이싱
리스트에서의 슬라이싱과 동일하게 사용하면 된다.
```python
arr1 = np.array([2, 5, 6, 7, 9, 11])
arr1[2:5] # [6 7 9]
```

### 모듈 행렬 연산
```python
arr = np.array([1, 2, 3, 4, 5, 6])
arr = arr + 2 # [3 4 5 6 7 8]
```
 - 다음과 같이 모든 원소에 대한 연산을 간단하게 수행할 수 있다. 뺄셈, 곱셈, 나눗셈 모두 동일하게 가능하다.
```python
arr1 = np.arange(0, 10)
arr2 = np.arange(10, 20)
arr1 + arr2 # [10 12 14 16 18 20 22 24 26 28]
```
 - 두 size가 같은 배열의 동일한 인덱스에 위치한 원소끼리 연산을 할 수 있다.
```python
arr = np.array([1, 2, 3, 4, 5, 6])
np.where(arr >= 4) # [3 4 5]
```
- 배열의 각 원소에 Condition을 걸어 참인 원소의 인덱스만 return할 수 있다.

#### 행렬 곱셈
numpy 모듈의 dot()메소드나 연산자 @를 사용하여 배열 간 행렬 곱을 수행할 수 있다.
```python
A = np.array([
              [1, 1, 2],
              [2, 3, 1],
              [3, 5, 1]
])
B = np.array([
              [5, 2, 1],
              [-1, 3, 4],
              [6, 3, 5]
])
np.dot(A, B) # A@B도 동일한 연산을 수행한다.
```
```python
array([[16, 11, 15],
       [13, 16, 19],
       [16, 24, 28]])
```

#### 전치 행렬;transpose
numpy 모듈의 transpose() 또는 T 메소드를 사용하여 전치 행렬을 만들 수 있다.
```python
np.transpose(A) # A.T 도 동일
```
```python
array([[1, 2, 3],
       [1, 3, 5],
       [2, 1, 1]])
```
#### 단위 행렬; indentity maxtrix
numpy 모듈의 identity() 메소드를 사용하여 단위 행렬을 만들 수 있다.
```python
np.identity(3) # np.identity(size) size*size 단위행렬
```
```python
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```
#### 역행렬; inverse matrix
numpy 모듈의 linalg.pinv()메소드를 사용하여 역행렬을 만들 수 있다.
```python
A_inv = np.linalg.pinv(A)
A_inv
```
```python
array([[-2.,  9., -5.],
       [ 1., -5.,  3.],
       [ 1., -2.,  1.]])
```
```python
A@A_inv
```
 - 자신과 인버스의 행렬곱은 단위행렬이다. 계산에서 소수점에 대한 연산이 정확이 0이 될 수 없음을 확인할 수 있다.
```python
array([[ 1.00000000e+00,  8.88178420e-15, -5.55111512e-15],
       [-1.33226763e-15,  1.00000000e+00, -4.77395901e-15],
       [-1.33226763e-15,  6.21724894e-15,  1.00000000e+00]])
```

### 모듈 통계 연산
#### 최대, 최소
```python
arr = np.array([1, 2, 3, 4, 5, 6])
arr.max() # 6
arr.min() # 1
```
#### 평균
```python
arr.mean() #3.5
```
#### 중앙값
```python
np.median(arr) #3.5
```
 - 중앙값이 3 과 4 두개여서 두개의 평균이 산출됨
#### 분산, 표준편차
```python
arr.var() # 2.9166666666666665
arr.std() # 1.707825127659933
