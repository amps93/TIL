# Pandas 데이터 분석 실습

* Feature Selection
  * pca : 독립변수들끼리의 상관관계만으로만 차원을 축소
  * rfe, regression : 독립변수와 종속변수(타겟변수)와의 관계를 통해 차원을 축소시킨다
* pca는 자체적으로 공분산 값을 구해서 Eigen Value값을 얻은 후 이를 비교해 위에서부터 큰 값을 리턴한다

## 1. DB에서 데이터 불러오기

```python
import pymysql.cursors
import pandas as pd
import numpy as np
from numpy import isnan
from sklearn.impute import SimpleImputer
from sklearn.feature_selection import RFE, SelectKBest, f_regression
# from sklearn.tree import DecisionTreeClassifier #타겟 변수가 0과 1일 때
from sklearn.svm import SVR #타겟 변수가 numeric 일 때
from sklearn.preprocessing import MinMaxScaler, StandardScaler
from sklearn.datasets import make_classification, make_regression
from sklearn.decomposition import PCA

# 1. DB에서 데이터 불러오기
conn = pymysql.connect(host='localhost', user='amps',
                       password='123123', db='tip', charset='utf8',
                       autocommit=True, cursorclass=pymysql.cursors.DictCursor)
try:
   with conn.cursor() as curs:
      sql = "SELECT * FROM tips;"
      curs.execute(sql)
      rs = curs.fetchall()

      # DB에서 받아온 값을 DataFrame에 넣음
      df = pd.DataFrame(rs)
      # print(df)
finally:
   conn.close()

# print(df.head())
```



## 2. 변수 인코딩

```python
# 2. 변수 인코딩
#범주형 변수 연속형 변수로 인코딩
df['sex'].replace({'Female':0, 'Male':1}, inplace = True)
df['smoker'].replace({'No':0, 'Yes':1}, inplace = True)
df['day'].replace({'Thur':0, 'Fri':1, 'Sat':2, 'Sun':3}, inplace = True)
df['time'].replace({'Lunch':0, 'Dinner':1}, inplace = True)
# df.replace('',np.nan, inplace=True) #''데이터가 있으면 nan값으로 대체 (공백 데이터가 있으면 아래 impute과정에서 오류 발생)

print(df.isnull().sum()) # df에 null값이 있는지 확인
```



## 3. nan 데이터 median 값으로 대체

```python
# 3. nan 데이터 median 값으로 대체
data = df.values # DataFrame to array
imputer = SimpleImputer(strategy='median') #중앙값으로 null값 대체
imputer.fit(data)
data_trans = imputer.transform(data) #null값이 없는 imputed dataset
# data_trans[:,5] #데이터에 null값이 있는지 확인
print('flatten 후 null값 확인 : ',sum(isnan(data_trans).flatten())) #데이터에 null값이 있는지 확인 / 코드 해석 : flatten 함수를 사용하여 데이터를 일렬로 펼친 후 isnan함수를 sum하여 null값의 합계 확인
```



## 4. 종속변수와 독립변수 분류

```python
# 여기서는 tip이 종속변수(타겟변수)
y=df['tip']
X=df.drop('tip',axis=1) #tip column 삭제 / axis1 : 열
# X.describe()
# y.describe()
```



## 5. Data Transform(정규화)

```python
#5. Data Transform(정규화)
#현재 데이터분석 사례에서는 사용하지 않는다
#MINMAXSCALER
trans = MinMaxScaler()
# print(data.shape)
X_norm = trans.fit_transform(data)
df_X_norm = pd.DataFrame(X_norm)
# print(df_X_norm.describe())

#StnadardScaler
sc = StandardScaler()
df_sc = sc.fit_transform(data)
df_trsform_sc = pd.DataFrame(df_sc)
# print(df_trsform_sc.describe().round())
```



## 6. Freature Selection(차원축소)

```python
#6. Feature Selection (차원축소)
#PCA
#define the transform
trans = PCA(n_components = 4) #feature를 4개만 뽑음
#transform the data
X_dim = trans.fit_transform(data_trans)
#summarize data after the transform
# print(X_dim[:3,:]) #4개의 feature의 첫 3줄이 나옴

#RFE
estimator = SVR(kernel='linear')
rfe = RFE(estimator, n_features_to_select=4) #feature를 4개만 뽑음
# print(data_trans.shape)
selector = rfe.fit(data_trans,y)
# print(selector.support_) #selector의 Ture/False값 반환
# print(selector.ranking_) #selector의 랭킹값 반환
#column 위치와 rank를 한번에 보여줌
for i in range(data_trans.shape[1]):
    print('column : %d, rank : %d' % (i, selector.ranking_[i]))

#Regression
fs = SelectKBest(score_func=f_regression, k=4) # 4 feature selection
# print(data_trans.shape)
# print(y.shape)
# apply feature selection
X_selected = fs.fit_transform(data_trans, y)
# print(X_selected.shape)
# print(pd.DataFrame(X_selected))
```

