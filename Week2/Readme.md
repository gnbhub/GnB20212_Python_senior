# 2주차 Pandas(cont'd)
pandas는 DataBase와 밀접하게 관련된 모듈이다.
### csv file?
comma separated values, 표 형태의 데이터를 말 그대로 (,)로 구분하여 저장하는 파일 형식이다.
<br>한 줄이 한 개의 행에 해당하며, 열 사이에는 쉼표(,)를 넣어 구분한다.
표의 형태를 직관적으로 나타내는 간단한 형식이라 이해하기 쉬우며, 소프트웨어로 처리하는 것도 쉽다. 텍스트 기반 형식이라 사람이 직접 읽고 수정하는 것도 가능하다.

이런 특징 때문에 DB에서 csv를 다루는 일이 많은데 pandas 모듈은 csv파일을 파이썬에서 읽을 수 있도록 한다.

## csv파일 불러오기
![a](https://user-images.githubusercontent.com/79446573/136019505-a7b3bb9e-7cc8-4512-ab01-f42d141b5c44.png)
<br> 구글 코랩 기준으로 파일 업로드를 통하여 런타임에서 파일에 접근할 수 있도록 한다.
<br> 구글 드라이브에 저장해놓고 접근하여도 되고, 코랩외의 환경이라면 Pc 저장소에서 불러올 수도 있다.
<br> sample.csv파일을 업로드한다.
```python
import pandas as pd
df = pd.read_csv('sample.csv') # ' ' 안에 경로가 들어가면 된다. ex 구글 드라이브or pc 저장소 파일위치
```
pd의 read_scv메소드를 이용하여 csv파일을 불러오면 바로 DataFrame type이 된다.<br>
![image](https://user-images.githubusercontent.com/79446573/136019888-6cd595d9-8191-41ac-89c4-4b8d486e0c28.png)
### csv파일 내에 column이 지정되어 있지 않은 경우
csv 파일의 첫줄을 column의 이름들로 받아들이는데, 열 이름이 없다면 다음과 같이 인자를 추가한다.<br>
![image](https://user-images.githubusercontent.com/79446573/136020204-0ff899c4-e141-447e-aa72-ccfb2c71fb91.png)
```python
df = pd.read_csv('sample.csv', header = None)
df
```
첫 줄부터 원소로 인식하였음을 확인할 수 있다.

### csv 파일 내에 행의 이름이 존재하는 경우
아무 인자가 없다면 0부터 줄마다 번호가 매겨지는데 파일에 index가 작성되어 있다면 다음과 같이 인자를 추가한다.
![image](https://user-images.githubusercontent.com/79446573/136022411-9b81b26f-4283-410a-8f47-7ba1a168e2d3.png)
```python
df = pd.read_csv('sample.csv', index_col = 0)
df
```
0번 컬럼을 인덱스 컬럼으로 받아들이겠다는 것인데, 컬럼의 이름이 있는 행은 이름이 필요 없다. 그래서 파일에서 A의 위치에 아무것도 없어야 하는데 A가 존재해서 컬럼이 꼬였음을 확인할 수 있다.
