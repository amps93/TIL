# Pandas 데이터 파일 읽고 쓰기

## 표 형식의 데이터 파일 읽기

* pd.read_csv(file_name, option)

| optinon            | 설명                                            |
| ------------------ | ----------------------------------------------- |
| index_col = 열이름 | 자동 인덱스 대신 특정 열 이름으로 파일을 불러옴 |
| encoding = 'utf-8' | utf-8 형식으로 파일을 불러옴                    |
| sep = 구분자       | 해당 구분자 옵션으로 파일을 불러옴              |



## 표 형식의 데이터를 파일로 쓰기

* pd.to_csv(file_name, option)

```python
import pandas as pd

#DataFrame 생성 후 index name을 User로 지정
df_WH = pd.DataFrame({'Weight' : [62,67,55,74],
                      'Height' : [165,177,160,180],}
                     , index = ['ID_1', 'ID_2', 'ID_3', 'ID_4'])
df_WH.index.name = 'User'
print(df_WH)
'
      Weight  Height
User                
ID_1      62     165
ID_2      67     177
ID_3      55     160
ID_4      74     180
'

#각 유저의 bmi 계산
bmi = df_WH['Weight']/(df_WH['Height']/100)**2
print(bmi)
'
User
ID_1    22.773186
ID_2    21.385936
ID_3    21.484375
ID_4    22.839506
dtype: float64
'

#bmi를 DataFrame에 추가
df_WH['BMI'] = bmi
print(df_WH)
'
      Weight  Height        BMI
User                           
ID_1      62     165  22.773186
ID_2      67     177  21.385936
ID_3      55     160  21.484375
ID_4      74     180  22.839506
'

df_WH.to_csv('저장 경로') #csv파일로 저장    
```

