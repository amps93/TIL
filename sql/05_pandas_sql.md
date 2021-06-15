# pandas를 sql처럼 사용하기

## SELECT

```python
import pandas as pd
import numpy as np

tips = pd.read_csv('tips.csv')
print(tips.head())
print()

#SELECT
print('*****SELECT*****')
'''
SELECT total_bill, tip, smoker, time
FROM tips
LIMIT 5;
'''
print(tips[['total_bill', 'tip', 'smoker', 'time']].head())
print()

#WHERE
print('*****WHERE*****')
'''
SELECT * 
FROM tips 
WHERE time = 'Dinner'
LIMIT 5;
'''
print(tips[tips['time'] == 'Dinner'].head())
print()

#time 컬럼의 Dinner이면 True 아니면 False를 준 후 value_counts를 통해 갯수 확인
is_dinner = tips['time'] == 'Dinner'
print(is_dinner.value_counts())
# print(tips[is_dinner].head())
print()

#Dinner 타임에 팁이 5$ 이상인 로우만 출력
'''
SELECT *
FROM tips
WHERE time = 'Dinner' AND tip > 5.00;
'''
print('***time = Dinner ,tips > 5.00$***')
print(tips[(tips['time'] == 'Dinner') & (tips['tip'] > 5.00)])
print()

#Null checking
print('***Null값 확인***')
frame = pd.DataFrame(
    {"col1": ["A", "B", np.NaN, "C", "D"], "col2": ["F", np.NaN, "G", "H", "I"]}
)
# print(frame)
'''
SELECT *
FROM frame
WHERE col1 IS NOT NULL;
'''
print(frame[frame["col1"].isna()])
print(frame[frame["col2"].isna()])
print('***col1에서 Null값 없는 데이터 출력***')
print(frame[frame["col1"].notna()])
print()
```



## GROUP BY

```python
#GROUP BY
print('*****GROUP BY*****')
'''
SELECT sex, count(*)
FROM tips
GROUP BY sex;
/*
Female     87
Male      157
*/
'''
print('***성별 카운트1***')
print(tips.groupby("sex").size())
print('***성별 카운트2***')
print(tips.groupby("sex")["total_bill"].count())
print('***성별에 따른 다른 컬럼 카운트***')
print(tips.groupby("sex").count())
print()

#Multiple fuction
'''
SELECT day, AVG(tip), COUNT(*)
FROM tips
GROUP BY day;
/*
Fri   2.734737   19
Sat   2.993103   87
Sun   3.255132   76
Thur  2.771452   62
*/
'''
print('***확장된 GROUP BY(agg 사용)***')
print(tips.groupby("day").agg({"tip": np.mean, "day": np.size}))
print()

#3차원 데이터 프레임
'''
SELECT smoker, day, COUNT(*), AVG(tip)
FROM tips
GROUP BY smoker, day;
/*
smoker day
No     Fri      4  2.812500
       Sat     45  3.102889
       Sun     57  3.167895
       Thur    45  2.673778
Yes    Fri     15  2.714000
       Sat     42  2.875476
       Sun     19  3.516842
       Thur    17  3.030000
*/
'''
print('***GROUP BY로 3차원 데이터 프레임 만들기***')
print(tips.groupby(["smoker", "day"]).agg({"tip": [np.size, np.mean]}))
```



## JOIN

```python
#JOIN
print('*****JOIN*****')
df1 = pd.DataFrame({"key": ["A", "B", "C", "D"], "value": np.random.randn(4)})
df2 = pd.DataFrame({"key": ["B", "D", "D", "E"], "value": np.random.randn(4)})

print('*****INNER JOIN*****')
'''
SELECT *
FROM df1
INNER JOIN df2
  ON df1.key = df2.key;
'''
print('merge함수 사용하여 INNER JOIN 하기(key값 기준으로)')
print(pd.merge(df1, df2, on='key'))

indexed_df2 = df2.set_index("key")
# print(indexed_df2)
print(pd.merge(df1, indexed_df2, left_on="key", right_index=True))
print()

#LEFT JOIN
print('*****LEFT JOIN*****')
'''
-- show all records from df1
SELECT *
FROM df1
LEFT OUTER JOIN df2
  ON df1.key = df2.key;
'''
print('merge함수 사용하여 LEFT JOIN 하기(key값 기준으로)')
print(pd.merge(df1, df2, on="key", how="left"))
print()

#RIGHT JOIN
print('*****RIGHT JOIN*****')
'''
-- show all records from df2
SELECT *
FROM df1
RIGHT OUTER JOIN df2
  ON df1.key = df2.key;
'''
print('merge함수 사용하여 RIGHT JOIN 하기(key값 기준으로)')
print(pd.merge(df1, df2, on="key", how="right"))
print()

#FULL JOIN
print('*****FULL JOIN*****')
'''
-- show all records from both tables
SELECT *
FROM df1
FULL OUTER JOIN df2
  ON df1.key = df2.key;
'''
print('merge함수 사용하여 FULL JOIN 하기(key값 기준으로)')
print(pd.merge(df1, df2, on="key", how="outer"))
print()
```



## UNION

```python
#UNION
df1 = pd.DataFrame(
    {"city": ["Chicago", "San Francisco", "New York City"], "rank": range(1, 4)}
)
df2 = pd.DataFrame(
     {"city": ["Chicago", "Boston", "Los Angeles"], "rank": [1, 4, 5]}
)
'''
SELECT city, rank
FROM df1
UNION ALL
SELECT city, rank
FROM df2;
/*
         city  rank
      Chicago     1
San Francisco     2
New York City     3
      Chicago     1
       Boston     4
  Los Angeles     5
*/
'''
print('*****UNION*****')
print('concat 함수 사용하여 UNION 수행하기')
print(pd.concat([df1, df2]))

print('concat 함수 사용하여 UNION ALL 수행하기')
print(pd.concat([df1, df2]).drop_duplicates())
print()
```



## ETC

```python
#ETC
print('*****기타 SQL 분석 및 집계 함수 사용하기*****')
'''
SELECT * FROM tips
ORDER BY tip DESC
LIMIT 10 OFFSET 5;
'''
print('nlargest 사용하여 tip 컬럼 15개까지 내림차순 정렬')
print(tips.nlargest(10 + 5, columns="tip"))
print()

'''
-- Oracle's ROW_NUMBER() analytic function
SELECT * FROM (
  SELECT
    t.*,
    ROW_NUMBER() OVER(PARTITION BY day ORDER BY total_bill DESC) AS rn
  FROM tips t
)
WHERE rn < 3
ORDER BY day, rn;
'''
print('Top n rows per group')
print(tips.assign(rn=tips.sort_values(['total_bill'], ascending=False)
                  .groupby(['day'])
                  .cumcount()
                  +1
                )
      .query('rn < 3')
      .sort_values(['day', 'rn'])
)
print()
```



## UPDATE

```python
#UPDATE
print('*****UPDATE*****')
'''
UPDATE tips
SET tip = tip*2
WHERE tip < 2;
'''
print('tip컬럼의 값이 2보다 작으면 2를 곱한 후 UPDATE')
# tips.loc[tips["tip"] < 2, "tip"] *= 2
# print(tips)
print()
```



### DELETE

```python
#DELETE
print('*****DELETE*****')
'''
DELETE FROM tips
WHERE tip > 9;
'''
print('tip칼럼의 값이 9이하인 값만 남겨둠')
tips = tips.loc[tips["tip"] <= 9]
print(tips)
```

