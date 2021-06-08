# Pandas 데이터 통합하기

## 세로 방향으로 통합하기

* df1.append(df2, ignore_index=True)

```python
import pandas as pd
import numpy as np

df1 = pd.DataFrame({'Class1' : [95,92,98,100],
                    'Class2' : [91,93,97,99]})

df2 = pd.DataFrame({'Class1' : [87,89],
                    'Class2' : [85,90]})

print(df1.append(df2))
'
   Class1  Class2
0      95      91
1      92      93
2      98      97
3     100      99
0      87      85
1      89      90
'

print(df1.append(df2,ignore_index=True))
'
   Class1  Class2
0      95      91
1      92      93
2      98      97
3     100      99
4      87      85
5      89      90
'

#columns이 같지 않은 DataFrame 데이터를 append()를 이용해 추가하면 데이터가 없는 부분은 Nan으로 채워짐
df3 = pd.DataFrame({'Class1' : [96,83]})

print(df2.append(df3))
'
   Class1  Class2
0      87    85.0
1      89    90.0
0      96     NaN
1      83     NaN
'
```



## 가로 방향으로 통합하기

* df1.join(df2)

```python
df4 = pd.DataFrame({'Class3' : [93,91,95,98]})

print(df1.join(df4))
'
   Class1  Class2  Class3
0      95      91      93
1      92      93      91
2      98      97      95
3     100      99      98
'

#index의 크기가 같지 않은 DataFrame 데이터를 join()을 이용해 추가하면 데이터가 없는 부분은 Nan으로 채워짐
df5 = pd.DataFrame({'Class4' : [82,92]})

print(df1.join(df5))
'
   Class1  Class2  Class4
0      95      91    82.0
1      92      93    92.0
2      98      97     NaN
3     100      99     NaN
'
```



## 특정 열을 기준으로 통합하기

* df_left_data.merge(df_right_data)

```python
df_A_B = pd.DataFrame({'판매월' : ['1월','2월','3월','4월'],
                       '제품A' : [100,150,200,130],
                       '제품B' : [90,110,140,170]})

df_C_D = pd.DataFrame({'판매월' : ['1월','2월','3월','4월'],
                       '제품C' : [112,141,203,134],
                       '제품D' : [90,110,140,170]})

print(df_A_B.merge(df_C_D)) #판매월 기준으로 통합
  판매월  제품A  제품B  제품C  제품D
0  1월  100   90  112   90
1  2월  150  110  141  110
2  3월  200  140  203  140
3  4월  130  170  134  170
```

* 특정 열 기준으로 일부만 공통된 값을 갖는 경우 통합
* df_left_data.merge(df_right_data, how = merge_method, on=key_label)

| how 선택 인자 | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| left          | 왼쪽 데이터는 모두 선택하고 지정된 열(key)에 값이 있는 오른쪽 데이터를 선택 |
| right         | 오른쪽 데이터는 모두 선택하고 지정된 열(key)에 값이 있는 왼쪽 데이터를 선택 |
| outer         | 지정된 열(key)을 기준으로 왼쪽과 오른쪽 데이터를 모두 선택   |
| inner         | 지정된 열(key)을 기준으로 왼쪽과 오른쪽 데이터 중 공통 항목만 선택(기본값) |

```python
df_left = pd.DataFrame({'key' : ['A','B','B'], 'left' : [1,2,3]})
df_right = pd.DataFrame({'key' : ['A','B','D'], 'right' : [4,5,6]})

#left
print(df_left.merge(df_right, how = 'left', on = 'key'))
'
  key  left  right
0   A     1      4
1   B     2      5
2   B     3      5
'
#right
print(df_left.merge(df_right, how = 'right', on = 'key'))
'
  key  left  right
0   A   1.0      4
1   B   2.0      5
2   B   3.0      5
3   D   NaN      6
'
#outer
print(df_left.merge(df_right, how = 'outer', on = 'key'))
'
  key  left  right
0   A   1.0      4
1   B   2.0      5
2   B   3.0      5
3   D   NaN      6
'
#inner
print(df_left.merge(df_right, how = 'inner', on = 'key'))
'
  key  left  right
0   A     1      4
1   B     2      5
2   B     3      5
'
```

