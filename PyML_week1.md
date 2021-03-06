파이썬 머신러닝 가이드 1장
==========================

머신러닝의 대표 라이브러리 : 넘파이, 판다스.
---------------------------------------------

넘파이 ndarray
---------------
​> 숫자, 문자열, 불 값 모두 가능.

> 데이터타입은 같은 것끼리만 가능

> astype 사용 가능

> 생성할 때 함수 ( arrange, zeros, ones )

> 차원과 크기 변경 : reshape

​

​

넘파이 인덱싱
------------

### 추출

### 슬라이싱  ':'을 사용해 시작과 종료

  기호 앞에 시작 인덱스 생략시 처음인 0으로 간주.  기호뒤를 생략할 경우 마지막까지

### 팬시인덱싱

 인덱스 집합을 정하면 이를 반환

### 불린인덱싱

 조건필터링을 적용할 수 있는 인덱싱.

 ndarray의 필터링 조건을 []안에 넣고, True에 해당하는 인덱스 값을 저장한다.

 인덱스 값을 저장한 데이터 셋으로 ndarray 조회

 

행렬 정렬
---------

 ### np.sort() : 원래의 행렬은 유지, 정렬된 행렬 반환
### ndarray.sort() : 원래의 행렬 자체를 정렬한 상태로 바꿔 저장하고 반환값이 없다.
### np.argsort() : 원본 행렬의 정렬 시의 행렬 인덱스 값



데이터핸들링 > 판다스
----------------------

### DataFrame 과 리스트, 딕셔너리, 넘파이 ndarray 상호변환

Dataframe -> 2차원 데이터
      즉 2차원 이하의 데이터만 Dataframe으로 변환가능



리스트, 넘파이 ndarray  -> 칼럼명 지정해주어야. ( 지정하지않으면 자동할당) 

import numpy as np

colname=['col1']

list1 = [1,2,3]
array=np.array(list1)

#리스트로 dataframe 생성
df_list=pd.DataFrame(list1, columns=colname)

#넘파이 ndarray를 이용해 dataframe 생성
df_array1= pd.DataFrame(array, columns=colname)

#딕셔너리를 이용한 변환
#Key는 문자열 칼럼명으로 매핑, Value는 리스트형 칼럼 데이터로 매핑
dict={'col1':[1,11], 'col2':[2,22], 'col3' : [3,33]}
df_dict= pd.DataFrame(dict)

#dataframe을 ndarray로 변환       //  values 이용
array=df_dict.values

#dataframe을 리스트로 변환
array=df_dict.values.tolist()

#dataframe을 딕셔너리로 변환
dict= df_dict.to_dict('list')
​

​

DataFrame 데이터 삭제

DataFrame.drop(labels=None, axis=0, index=None, columns=Nones, level=None, inplace=False, errors='raise')
axis 0  - > 세로 ( 로우방향)

axis 1  - > 가로 ( 칼럼방향)

​

(ex) Age_0 칼럼을 삭제 

drop_df= titanic_df.drop('Age_0', axis=1)
inplace가 false로 설정될 경우, 삭제된 결과 데이터프레임을 반환.

true일 경우 , 자신의 데이터프레임에서 삭제됨.

​

Index 객체
----------
Dataframe, Series의 레코드를 고유하게 식별. 

reset_index()  수행 시 인덱스가 연속숫자로 할당, 기존 인덱스는 index로 추가.

​

데이터셀렉션 및 필터링
-----------------------
위치기반 : 0부터 시작하는 행, 열의 위치좌표

명칭기반 : DataFrame의 인덱스나 칼럼명으로 접근


- DataFrame의 []연산자 > 칼럼 지정가능한 연산자. // 슬라이싱 가능하지만 비추천

- DataFrame ix[] ->  행위치지정, 열위치지정으로 원하는 위치의 데이터 추출  / 위치기반, 명칭기반 모두 가능

- DataFrame iloc[] -> df.iloc[1,1] -> 위치기반 인덱싱 값 입력 ( 명칭입력 시 오류 )

- DataFrame loc[] -> 명칭기반으로 데이터 추출. index가 숫자일 경우 숫자로도 가능.



불린인덱싱
-----------
ix,iloc,loc > 상대적으로 명확히 인덱싱 지정

조건으로 불러오는 불린을 더 자주 사용.



정렬- sort_values()
---------------------
ascending= True 일 경우 오름차순, False일 경우 내림차순,

inplace=False 가 기본.



Aggregation
-------------
mean, max, min, sum, count 적용

df.count() 적용시 모든 칼럼에 일괄 적용


groupby
---------
groupby(by='Pclass') 를 호출 -> Pclass 칼럼 기준으로 GroupBy된 객체 반환



결손데이터처리
-------------
isna()         : 데이터가 NaN인지 아닌지를 알려준다. True or False로 반환

fillna()       : 결손데이터 대체



apply lambda 식으로 데이터가공
------------------------------
데이터가공 기능. 

lamba x : x**2              > :로 입력입자와 반환 입력인자 분리. // 반환 입력인자에는 조건 식 가능 ( if , else 가능. )

​

​
