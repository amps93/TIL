# Pandas

## DataFrame

* 2차원 데이터 생성
* df = pd.DataFrame(data, [, index = index_data, columns = columns_data])

```python
import numpy as np
import pandas as pd

df = pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]])
print(df)
'
   0  1  2
0  1  2  3
1  4  5  6
2  7  8  9
'

#numpy 사용하여 DataFrame 생성하기
import numpy as np
import pandas as pd

data_list = np.array([[10,20,30],[40,50,60],[70,80,90]])
print(pd.DataFrame(data_list))
'
    0   1   2
0  10  20  30
1  40  50  60
2  70  80  90
'

#index, coldata = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
index_date = pd.date_range('2019-09-01', periods=4)
columns_list = ['A','B','C']
print(pd.DataFrame(data, index = index_date, columns=columns_list))umns 지정해 생성
'
             A   B   C
2019-09-01   1   2   3
2019-09-02   4   5   6
2019-09-03   7   8   9
2019-09-04  10  11  12
'

#딕셔너리 이용하여 DataFrame 만들기
table_data = {'연도': [2015,2016,2016,2017,2017],
            '지사':['한국','한국','미국','미국','미국'],
            '고객수':[200,250,450,300,500]}
df = pd.DataFrame(table_data)
print(df)
'
     연도  지사  고객수
0  2015  한국  200
1  2016  한국  250
2  2016  미국  450
3  2017  미국  300
4  2017  미국  500
'

print(df.index)
RangeIndex(start=0, stop=5, step=1)

print(df.columns)
Index(['연도', '지사', '고객수'], dtype='object')

print(df.values)
[[2015 '한국' 200]
 [2016 '한국' 250]
 [2016 '미국' 450]
 [2017 '미국' 300]
 [2017 '미국' 500]]
```



## 데이터 요약

```python
import pandas as pd

data = {'봄' : [256.5,264.3,215.9,223.2,312.8],
      '여름' : [770.6,567.5,599.8,387.1,446.2],
      '가을' : [363.5,231.2,293.1,247.7,381.6],
      '겨울' : [139.3,59.9,76.9,109.1,108.1]}
columns_list = ['봄', '여름', '가을','겨울']
index_list = ['2012','2013','2014','2015','2016']

df = pd.DataFrame(data, columns=columns_list, index =index_list)
print(df)
'
          봄     여름     가을     겨울
2012  256.5  770.6  363.5  139.3
2013  264.3  567.5  231.2   59.9
2014  215.9  599.8  293.1   76.9
2015  223.2  387.1  247.7  109.1
2016  312.8  446.2  381.6  108.1
'

#df.info()
print(df.info())
'
<class 'pandas.core.frame.DataFrame'>
Index: 5 entries, 2012 to 2016
Data columns (total 4 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   봄       5 non-null      float64
 1   여름      5 non-null      float64
 2   가을      5 non-null      float64
 3   겨울      5 non-null      float64
dtypes: float64(4)
memory usage: 200.0+ bytes
None
'

#df.describe()
print(df.describe())
'
                봄          여름          가을          겨울
count    5.000000    5.000000    5.000000    5.000000
mean   254.540000  554.240000  303.420000   98.660000
std     38.628267  148.888895   67.358496   30.925523
min    215.900000  387.100000  231.200000   59.900000
25%    223.200000  446.200000  247.700000   76.900000
50%    256.500000  567.500000  293.100000  108.100000
75%    264.300000  599.800000  363.500000  109.100000
max    312.800000  770.600000  381.600000  139.300000
'

#df.profile_report
import pandas_profiling

print(df.profile_report)
```

