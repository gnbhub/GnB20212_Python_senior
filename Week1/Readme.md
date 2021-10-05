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
```

## Pandas?
 - 파이썬 언어로 작성된 데이터를 분석 및 조작하기 위한 소프트웨어 라이브러리이다. 
 - 수치형 테이블과 시계열 데이터를 조작하고 운영하기 위한 데이터를 제공한다.
 - 이름은 계량 경제학에서 사용되는 용어인 'PANel DAta'의 앞 글자를 따서 지어졌다. 
 - R에서 사용되던 data.frame 구조를 본뜬 DataFrame이라는 구조를 사용하기 때문에, R의 data.frame에서 사용하던 기능 상당수를 무리없이 사용할 수 있도록 만들었다.

### Pandas 모듈
pandas 모듈은 numpy모듈의 설치가 선행되어야 한다.
```python
import pandas
```
편의를 위해 pd로 축약해서 사용한다.
```python
import pandas as pd
```
※ numpy 모듈의 ndarray는 행렬의 모든 요소가 동일한 자료형이어야 한다.<br>
하지만 pandas 모듈의 DataFrame은 다양한 자료형을 담을 수 있다.

### 2차원 배열 생성
```python
arr = [['first', 1], ['second', 2], ['third', 3]]
arr = pd.DataFrame(arr)

arr
```
![image](https://user-images.githubusercontent.com/79446573/135752061-e3cc45ea-0136-41c7-a79d-4f725b39c765.png)
<br> 3 by 2 행렬을 선언한 후에 DataFrame형태로 바꿔주는것이다. 지금 상황에선 column과 row에 이름이 단순히 0과 1로 지정되어있는것을 확인할 수 있다.

### columns에 이름 정하기
column은 데이터베이스에서 속성(Attribute)이나 필드(Field)로 불린다.
```python
arr = [['first', 1], ['second', 2], ['third', 3]]
arr = pd.DataFrame(arr, columns = ['Data1', 'Data2'])

arr
```
![image](https://user-images.githubusercontent.com/79446573/135752208-97e80552-0451-48f9-a807-46c2150d7f91.png)
<br> column의 이름이 `Data1`,`Data2`로 지정된것을 확인할 수 있다. 
#### column 이름 출력
```python
arr.columns
```
```python
Index(['Data1', 'Data2'], dtype='object')
```
### 각 필드의 자료형 확인
dtypes 메소드를 통해 각 필드에 해당하는 자료형을 확인해볼 수 있다.
```python
arr.types
```
```python
Data1    object
Data2     int64
dtype: object
```
### row에 이름 정하기
row는 데이터베이스에서 레코드(Record)로 불린다.
```python
arr = [['first', 1], ['second', 2], ['third', 3]]
arr = pd.DataFrame(arr, index = ['Data1', 'Data2', 'Data3'])

arr
```
![image](https://user-images.githubusercontent.com/79446573/135752305-210ca7c4-0fa0-4f18-8d3c-eec7816c5896.png)
<br> row의 이름이 `Data1`,`Data2`,`Data3`로 지정된것을 확인할 수 있다.
#### row 이름 출력
```python
arr.index
```
```python
Index(['Data1', 'Data2', 'Data3'], dtype='object')
```

### Pandas DataFrame 자료형 생성 및 변환
List, numpy array(ndarray), dict 자료형 모두 DataFrame자료형으로 변환할 수 있다.
#### List to DataFrame
```python
arr = [['A', 1], ['B', 2], ['C', 3]]
df = pd.DataFrame(arr)
type(arr)
```
```python
list
```
```python
type(df)
```
```python
pandas.core.frame.DataFrame
```

#### numpy array to DataFrame
```python
arr = [['A', 1], ['B', 2], ['C', 3]]
arr = np.array(arr)
df = pd.DataFrame(arr)

type(arr)
```
```python
numpy.ndarray
```
```python
type(df)
```
```python
pandas.core.frame.DataFrame
```
리스트를 ndarray로 변환하여 DataFrame으로 바꿀수도 있고 리스트 그대로 DataFrame으로 바꿀수 있음을 확인할 수 있다.

#### dict to DataFrame
dict의 Key에는 columns의 이름을 쓰고, 해당 column의 값들을 List, numpy array 또는 panda Series의 자료형으로 사전의 value에 넣어주면 된다.
```python
dict = {
    'A' : ['a1', 'a2', 'a3'],
    'B' : ['b1', 'b2', 'b3'],
    'C' : ['c1', 'c2', 'c3']
}
df = pd.DataFrame(dict)
df
```
![image](https://user-images.githubusercontent.com/79446573/135753077-934f6361-1cf3-41a3-afa0-3d7ee0835474.png)
```python
type(dict)
```
```python
dict
```
```python
type(df)
```
```python
pandas.core.frame.DataFrame
```

#### 원소 형변환
특정 요소의 자료형을 변환하기 위해서 astype 메소드를 사용한다.
```python
df = pd.DataFrame([True, True, False, False, True])
type(df)
```
```python
pandas.core.frame.DataFrame
```
```python
df = df.astype(int)
df
```
![image](https://user-images.githubusercontent.com/79446573/135753265-d3bcbf6b-425a-4a52-aab0-7a7ce18bc97a.png)
<br> 부울 타입 원소들이 정수형으로 변환된것을 확인할 수 있다.

## HW 1
week1 폴더 내의 hw1파일을 확인하여 따라 작성해보기! Ln(3) 이후의 코드에 대해 다 알려 하지 않아도 좋음.
구글 코랩, 파이참 등등 편한 프로그램 이용
