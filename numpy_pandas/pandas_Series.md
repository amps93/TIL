# Pandas

## Series

* 라벨을 갖는 1차원 데이터 생성
* s = pd.Series(seq_data)

```python
import pandas as pd

s1 = pd.Series([10,20,30,40,50])
print(s1)
'
0    10
1    20
2    30
3    40
4    50
dtype: int64
'
print(s1.index)
'RangeIndex(start=0, stop=5, step=1)'

print(s1.values)
'[10 20 30 40 50]'
```

* 아래와 같이 인덱스 추가 가능
* s = pd.Series(seq_data, index = index_seq)

```python
index_data = ['20181007','20181008','20181009','20181010']
s4 = pd.Series([200,195,np.nan,205], index=index_data)
print(s4)
'
20181007    200.0
20181008    195.0
20181009      NaN
20181010    205.0
dtype: float64
'
```

* 딕셔너리 데이터를 Series에 사용하기
* s = pd.Series(dict_data)

```python
s5 = pd.Series({'국어':100,'영어':80,'수학':90})
print(s5)
'
국어    100
영어     80
수학     90
dtype: int64
'
```

