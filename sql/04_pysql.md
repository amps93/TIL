# pysql

* python에서 sql 사용하기

```python
import pymysql.cursors
import pandas as pd

connection = pymysql.connect(host='localhost',
        user='amps',
        password='123123',
        db='tip',
        charset='utf8',
        cursorclass=pymysql.cursors.DictCursor)
try:
    with connection.cursor() as cursor:
        # Read a single record
        #sql = "SELECT `id`, `password` FROM `users` WHERE `email`=%s"
        # sql = "SELECT total_bill FROM tip.tips WHERE tip >= 7;"
        sql = "SELECT count(total_bill) FROM tip.tips WHERE tip >= 7;"
        cursor.execute(sql)
        result = cursor.fetchone()
        print(result)
finally:
    connection.close()


# MySQL DB에서 데이터 받아와서 DataFrame에 저장
conn = pymysql.connect(host='localhost', user='amps',
                       password='123123', db='tip', charset='utf8',
                       autocommit=True, cursorclass=pymysql.cursors.DictCursor)
try:

   with conn.cursor() as curs:
      sql = "SELECT total_bill FROM tip.tips WHERE tip >= 7;"
      curs.execute(sql)
      rs = curs.fetchall()

      # DB에서 받아온 값을 DataFrame에 넣음
      df = pd.DataFrame(rs)
      print(df)
      df.hist()

finally:

    conn.close()


# MySQL DB에서 데이터 받아와서 DataFrame에 저장
conn = pymysql.connect(host='localhost', user='amps',
                       password='123123', db='classicmodels', charset='utf8',
                       autocommit=True, cursorclass=pymysql.cursors.DictCursor)

sql="select customers.state, customers.customerName, payments.checkNumber from customers LEFT JOIN payments on customers.customerNumber = payments.customerNumber where payments.paymentDate >= '2004-10-06';"

try:

   with conn.cursor() as curs:
      curs.execute(sql)
      rs = curs.fetchall()

      # DB에서 받아온 값을 DataFrame에 넣음
      df = pd.DataFrame(rs)
      print(df)
      # df.to_csv('query_car.csv')

finally:

    conn.close()
```

