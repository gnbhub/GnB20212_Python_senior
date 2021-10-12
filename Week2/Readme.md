# 2주차 Pandas(cont'd)
pandas는 DataBase와 밀접하게 관련된 모듈이다.
### csv file?
comma separated values, 표 형태의 데이터를 말 그대로 (,)로 구분하여 저장하는 파일 형식이다.
<br>한 줄이 한 개의 행에 해당하며, 열 사이에는 쉼표(,)를 넣어 구분한다.
표의 형태를 직관적으로 나타내는 간단한 형식이라 이해하기 쉬우며, 소프트웨어로 처리하는 것도 쉽다. 텍스트 기반 형식이라 사람이 직접 읽고 수정하는 것도 가능하다.

이런 특징 때문에 DB에서 csv를 다루는 일이 많은데 pandas 모듈은 csv파일을 파이썬에서 읽을 수 있도록 한다.

## csv파일 불러오기
<img src="https://user-images.githubusercontent.com/79446573/136019505-a7b3bb9e-7cc8-4512-ab01-f42d141b5c44.png" width="50%" height="50%"></html>
<br> 구글 코랩 기준으로 파일 업로드를 통하여 런타임에서 파일에 접근할 수 있도록 한다.
<br> 구글 드라이브에 저장해놓고 접근하여도 되고, 코랩 외의 환경이라면 Pc 저장소에서 불러올 수도 있다.
<br> sample.csv파일을 업로드한다.
```python
import pandas as pd
df = pd.read_csv('sample.csv') # ' ' 안에 경로가 들어가면 된다. ex 구글 드라이브or pc 저장소 파일위치
```
pd의 read_scv메소드를 이용하여 csv파일을 불러오면 바로 DataFrame type이 된다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136019888-6cd595d9-8191-41ac-89c4-4b8d486e0c28.png" width="30%" height="30%"></html>

### csv파일 내에 column이 지정되어 있지 않은 경우
csv 파일의 첫줄을 column의 이름들로 받아들이는데, 열 이름이 없다면 다음과 같이 인자를 추가한다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136020204-0ff899c4-e141-447e-aa72-ccfb2c71fb91.png" width="30%" height="30%"></html>
```python
df = pd.read_csv('sample.csv', header = None)
df
```
첫 줄부터 원소로 인식하였음을 확인할 수 있다.

### csv 파일 내에 행의 이름이 존재하는 경우
아무 인자가 없다면 0부터 줄마다 번호가 매겨지는데 파일에 index가 작성되어 있다면 다음과 같이 인자를 추가한다.
<img src="https://user-images.githubusercontent.com/79446573/136022411-9b81b26f-4283-410a-8f47-7ba1a168e2d3.png" width="30%" height="30%"></html>
```python
df = pd.read_csv('sample.csv', index_col = 0)
df
```
0번 컬럼을 인덱스 컬럼으로 받아들이겠다는 것인데, 컬럼의 이름이 있는 행은 이름이 필요 없다. 그래서 파일에서 A의 위치에 아무것도 없어야 하는데 A가 존재해서 컬럼이 꼬였음을 확인할 수 있다.

## DataFrame 인덱싱
DataFrame에서 필요한 Data만을 선택하여 제어하기 위한 인덱싱을 알아보자.
### loc 메소드
loc 메소드를 사용하여 원하는 위치의 데이터를 가지고 올 수있다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136557280-8e81525b-94e7-4cdd-95fc-18583c417b11.png" width="30%" height="30%"></html>
```python
df.loc['A1', 'D'] # A1 row의 D 컬럼에 해당하는 데이터 불러오기
```
### iloc 메소드
특정 행과 열을 숫자로 인덱싱 할 수 있다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136557641-69f06073-040e-4678-be1b-8c06007ee60f.png" width="30%" height="30%"></html>
```python
df.iloc[1, 3]  # 1번 row의 3번 컬럼 데이터, 첫째 줄 3번째 열 데이터가 아니다! 둘째 줄 4번째 열 데이터다!
```
### 특정 row의 data 모두 출력
인덱싱을 :를 이용하면 원하는 부분을 출력할 수 있는데, 숫자 없이 `:`만 사용하면 해당되는모두를 가리키는 것이다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136558366-aef5777f-c898-4e0b-8ec1-a3ed268757ee.png" width="30%" height="30%"></html>
```python
df.loc['A2', : ]  # A2 행의 모든 data 출력
```
### 특정 column의 data 모두 출력
앞에서는 `,` 뒤에 `:`를 사용했다면 `,`앞에 :를 사용하여 column에 해당하는 data 모두를 가리킨다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136558888-d13019d3-a55d-408f-9469-273c7674047a.png" width="30%" height="30%"></html>
```python
df.loc[:, 'E']  # E 열의 모든 data 출력
```
### 여러개의 column data 출력
여러개의 열을 선택하고 싶다면 `[ ]`사이에 배열처럼 입력해 줄 수 있다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136559258-a7b4fb0e-4ebd-4cf6-b95d-b191b7b756b3.png" width="30%" height="30%"></html>
```python
df.loc[ : , ['C','D']]  # C,D column 모든 data출력
```
### column row slicing
`:`를 활용하여 모든 data를 가리도록 하였는데, 좌 우에 행이나 열의 이름이 들어가면 slicing이 가능하다.
#### 행 슬라이싱
<img src="https://user-images.githubusercontent.com/79446573/136561840-7b9c2a0e-8955-4fc7-857f-0d17500b2542.png" width="30%" height="30%"></html>
```python
df.loc['A2':,:] # , 좌측을 보면 'A2': 라 되어있는데 A2행 부터 모든 행을 선택한다.
```
#### 열 슬라이싱
<img src="https://user-images.githubusercontent.com/79446573/136562278-22f3bb26-7bcf-4ccb-bf4d-2be60b4fc48a.png" width="30%" height="30%"></html>
```python
df.loc[:, 'B':'D'] # , 우측에 'B':'D' 라 되어있는데 B열 부터 D열까지 선택한다.
```
loc 뿐만 아니라 iloc 메소드도 동일한 방법으로 슬라이싱 할 수 있다. 다만 행과 열의 이름이 아니라 행과 열의 인덱스로 제어해주면 되겠다.

### 데이터 변경하기
위에서 보았던 loc 메소드나 iloc 메소드를 이용해서 원하는 위치를 정하고 data를 변경할 수 있다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136563631-10344cd3-be78-42b6-bfe8-88cad1d605f5.png" width="30%" height="30%"></html>
```python
import pandas as pd
df = pd.read_csv('sample2.csv', index_col = 0)

df

df.loc['R2', 'C'] = 'changed' # R2행의 C열에 해당하는 데이터를 'changed'로 바꾼다.
df
```
#### row의 모든 데이터 변경하기
특정 행의 data 모두를 바꾸고 싶다면 다음과 같이 작성하면 된다.
<br> 행의 원소 갯수에 맞추어서 바꾸고 싶은 값을 선언하면 된다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136564365-58f852ee-426b-448f-894f-8941cc44aa1a.png" width="30%" height="30%"></html>

```python
df.loc['R2'] = ['K1', 'K2', 'K3', 'K4', 'K5', 'K6'] #R2 행의 데이터를 교환한다. 갯수가 맞아야 한다!
df
```
#### column의 모든 데이터 변경하기
<img src="https://user-images.githubusercontent.com/79446573/136564619-1170309a-89ae-4fc5-a961-cf4f1ecff2d3.png" width="30%" height="30%"></html>
```python
df.loc[:, 'D'] = ['K1', 'K2', 'K3', 'K4'] # D열의 데이터를 교환한다. 갯수가 맞아야 한다!
df
```
열의 원소 갯수에 맞추어서 바꾸고 싶은 값을 선언하면 된다.

#### ※동일하게 값을 지정하고 싶을 때
행이나 열의 데이터를 모두 동일하게 바꾸고 싶다면 바꾸고자 하는 데이터를 대입하면 된다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136565027-cec0efec-be8d-49b5-acdb-31d5ff255069.png" width="30%" height="30%"></html>
```python
df.loc[:, 'D'] = 'K' # D열의 데이터를 모두 'K'로 바꾼다.
df
```
row도 똑같이 바꿀수 있다.

### 대이터 추가 삭제
#### 행 추가
없는 행을 지정하여 데이터를 쓰면 새롭게 행이 추가된다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136566285-faadf18e-b077-499c-865f-83280817163e.png" width="30%" height="30%"></html>
```python
df.loc['R5'] = ['A5', 'B5', 'C5', 'D5', 'E5', 'F5'] # R5가 없다면 새로 생성될 것이고 있으면 R5값이 변경될 것이다.
df
```
열 추가도 마찬가지로 없는 열을 지정하여 데이터를 쓰면 새롭게 열이 추가된다.<br>
이 또한 원소 개수를 맞춰 주어야 한다.
#### 행 삭제, 열 삭제
drop() 메소드를 사용하여 행이나 열을 삭제할 수 있다.<br>
행을 삭제하고 싶다면 axis 인자의 값을 'index' 또는 0으로, 열을 삭제하고 싶다면 axis인자의 값을 'columns' 또는 1로 설정하면 된다.<br>
만일 df 변경하고 싶다면 inplace=True로 해주어야 한다. False라면 df값은 변하지않는다.<br>
<img src="https://user-images.githubusercontent.com/79446573/136567744-2b543db9-9d88-46f6-9695-e73da161223d.png" width="30%" height="30%"></html>
```python
df.drop('R3', axis='index', inplace=False) # axis가 index이므로 R3에 해당하는 행 삭제
```
<img src="https://user-images.githubusercontent.com/79446573/136569404-c7924d24-3024-4070-a450-1a5122e1f3bf.png" width="30%" height="30%"></html>
```python
df.drop('E', axis=1, inplace=False) # axis가 1이므로 E에 해당하는 열 삭제
```

## Quiz
<img src = "https://user-images.githubusercontent.com/79446573/136914740-f0ea8f8f-fb80-448c-a5d3-cea3047a5e27.png" width = "40%" height = "40%"></html>
<br>다음과 같은 DataFrame을 아래 사진처럼 만들기<br>
n번째 행 n번째 열의 원소를 1로 설정하기<br>
<img src = "https://user-images.githubusercontent.com/79446573/136915112-b0a962e8-2b39-4193-abc5-7a24d02a110e.png" width = "40%" height = "40%"></html>
<br>물론 행과 열을 동시에 다루는 일은 잘 없겠지만, 내용 학습으로 간단하게 해볼만해서 올립니다. 수동으로 바꾸기 금지


