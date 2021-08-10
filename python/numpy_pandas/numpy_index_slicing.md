# Numpy indexing&slicing



## 배열의 인덱싱

* 배열명[위치]

```python
a1 = np.array([0,10,20,30,40,50])
a1
'OUT: array([0,10,20,30,40,50])'

a1[0]
'OUT: 0'
a1[4]
'OUT: 40'
a1[5] = 70
a1
'OUT: array([0,10,20,30,40,70])'
```

* 배열명[[위치1,위치2,...,위치n]]

```python
a1[[1,3,4]]
a1
'OUT: array([10,30,40])'
```

* 배열명[행 위치, 열 위치]

```python
a2 = np.arange(10,100,10).reshape(3,3)
a2
'OUT: array([[10,20,30],
            [40,50,60],
            [70,80,90]])'
a2[0,2]
'OUT: 30'
a2[2,2]=95
'OUT: array([[10,20,30],
            [40,50,60],
            [70,80,95]])'
```

* 배열명[[행 위치1, 행 위치2, ..., 행 위치n],[열 위치1, 열위치2, ..., 열위치n]]

```python
a2[[0,2],[0,1]]
'OUT: array([10,80])'
```



## 배열의 슬라이싱

* 배열[시작 위치 : 끝 위치]

```python
b1 = np.array([0,10,20,30,40,50])
b1[1:4]
'OUT: array([10,20,30])'

b1[:3]
'OUT: array([0,10,20])'

b1[2:]
'OUT: array([20,30,40,50])'
```

* 배열[행 시작 위치:행 끝 위치, 열 시작 위치:열 끝 위치]

```python
b2 = np.arange(10,100,10).reshape(3,3)
b2
'OUT: array([[10,20,30],
            [40,50,60],
            [70,80,90]])'
       
b2[1:3,1:3]
'OUT: array([[50,60],
			[80,90]])'

b2[:3,1:]
'OUT: array([[20,30],
            [50,60],
            [80,90]])'

b2[1][0:2]
'OUT: array([40,50])'
```
