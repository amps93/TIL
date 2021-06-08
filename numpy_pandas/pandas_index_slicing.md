# Pandas indexing&slicing

## head()와 tail()

```python
import pandas as pd
import numpy as np

data = {'경부선 KTX' : [39060,39896,42005,43621,41702,41266,32427],
      '호남선 KTX' : [7313,6967,6873,6626,8675,10622,9228],
      '경전선 KTX' : [3627,4168,4088,4424,4606,4984,5570],
      '전라선 KTX' : [309,1771,1954,2244,3146,3945,5766],
      '동해선 KTX' : [np.nan,np.nan,np.nan,np.nan,2395,3786,6667]}
columns_list = ['경부선 KTX', '호남선 KTX', '경전선 KTX','전라선 KTX','동해선 KTX']
index_list = ['2011','2012','2013','2014','2015','2016','2017']

df = pd.DataFrame(data, columns=columns_list, index =index_list)
print(df)

'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2011    39060     7313     3627      309      NaN
2012    39896     6967     4168     1771      NaN
2013    42005     6873     4088     1954      NaN
2014    43621     6626     4424     2244      NaN
2015    41702     8675     4606     3146   2395.0
2016    41266    10622     4984     3945   3786.0
2017    32427     9228     5570     5766   6667.0
'

#df.head(n) : n 미설정시 기본값 5로 설정
print(df.head(2))
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2011    39060     7313     3627      309      NaN
2012    39896     6967     4168     1771      NaN
'

#df.tail(n)
print(df.tail(2))
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2016    41266    10622     4984     3945   3786.0
2017    32427     9228     5570     5766   6667.0
'
```



## indexing & slicing

### 행

* df[행 시작 위치:행 끝 위치]

```python
print(df[1:2])
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2012    39896     6967     4168     1771      NaN
'

print(df[2:5])
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2013    42005     6873     4088     1954      NaN
2014    43621     6626     4424     2244      NaN
2015    41702     8675     4606     3146   2395.0
''
```

* DataFrame 생성 시 인덱스를 지정했다면 아래와 같이 사용 가능
* df.loc[index_name]
* df.loc[start_index_name:end_index_name]
* df.iloc[index_pos]
* df.iloc[start_index_pos:end_index_pos]

```python
print(df.loc['2012'])
'
경부선 KTX    39896.0
호남선 KTX     6967.0
경전선 KTX     4168.0
전라선 KTX     1771.0
동해선 KTX        NaN
Name: 2012, dtype: float64
'

print(df.loc['2013':'2015'])
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2013    42005     6873     4088     1954      NaN
2014    43621     6626     4424     2244      NaN
2015    41702     8675     4606     3146   2395.0
'

print(df.iloc[1])
'
경부선 KTX    39896.0
호남선 KTX     6967.0
경전선 KTX     4168.0
전라선 KTX     1771.0
동해선 KTX        NaN
Name: 2012, dtype: float64
'

print(df.iloc[2:5])
'
      경부선 KTX  호남선 KTX  경전선 KTX  전라선 KTX  동해선 KTX
2013    42005     6873     4088     1954      NaN
2014    43621     6626     4424     2244      NaN
2015    41702     8675     4606     3146   2395.0
'
```



### 열

* df[column_name]
* `df[column_name][start_index_name:end_index_name]`
* `df[column_name][start_index_pos:end_index_pos]`

```python
print(df['경부선 KTX'])
'
2011    39060
2012    39896
2013    42005
2014    43621
2015    41702
2016    41266
2017    32427
Name: 경부선 KTX, dtype: int64
'

print(df['경부선 KTX']['2012':'2014']) #일반적인 경우와 달리 2014년 데이터까지 출력됨
'
2012    39896
2013    42005
2014    43621
Name: 경부선 KTX, dtype: int64
'     

print(df['경부선 KTX'][2:5])
'
2013    42005
2014    43621
2015    41702
Name: 경부선 KTX, dtype: int64
'
```

