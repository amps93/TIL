# Numpy



## numpy 배열 생성

```python
import numpy as np

#1차원 배열 생성
data1 = [0,1,2,3,4,5]
a1 = np.array[data1]
a1
'OUT: array([0,1,2,3,4,5])'

#2차원 배열 생성
data2 = [[1,2,3],[4,5,6],[7,8,9]]
a2 = np.array(data2)
a2
'OUT: array([[1,2,3],
            [4,5,6],
            [7,8,9]])''
 
#범위를 지정해 배열 생성
#arr_obj = np.arange(start,stop,step)
np.arange(0,10,2)
'OUT: array([0,2,4,6,8])'
np.arange(1,10)
'OUT: array([1,2,3,4,5,6,7,8,9])'
np.arange(5)
'OUT: array([0,1,2,3,4])'

#np.linspace() : start부터 stop까지 num개의 배열 생성
np.linspace(0,10,5)
'OUT: array([0., 2.5, 5., 7.5, 10.])'
```



## 특별한 형태의 배열 생성

```python
np.zeros(3,4) #3by4 0행렬
'OUT: array([[0., 0., 0., 0.],
            [0., 0., 0., 0.],
            [0., 0., 0., 0.]])'
        
np.ones(3,4) #3by4 1행렬
'OUT: array([[1., 1., 1., 1.],
            [1., 1., 1., 1.],
            [1., 1., 1., 1.]])'
        
np.eye(3) #3by3 단위행렬
'OUT: array([[1., 0., 0.],
            [0., 1., 0.],
            [0., 0., 1.]])'
```



## shape&reshape

```python
# shape : ndarray의 차원을 반환
data = np.arange(1,7)
data.shape
'OUT: (6,)'
data = np.array([[1,2,3],[4,5,6]])
data.shape
'OUT: (2,3)'

#reshape : 행렬의 차원을 바꾸는데 사용 / -1 입력 시 1차원 배열 반환
data = data = np.arange(1,7)
data.reshape(2,3)
#np.reshape(data,(2,3)) #위와 동일
'OUT: array([[1,2,3],
			[4,5,6]])'
data.reshape(-1)
'OUT: array([1,2,3,4,5,6])'
data.reshape(3,-1)
'OUT: array([[1,2],
            [3,4],
            [5,6]])'
```





## 배열의 데이터 타입 변환

```python
#num_arr = str_arr.astyep(dtype)
str_a1 = np.array(['1.567', '0.123', '5.123', '9', '8'])
num_a1 = str_a1.astype(float)
'OUT: array([1.567, 0.123, 5.123, 9, 8])'
str_a1.dtype
'OUT: dtype('<U5')' #유니코드
num_a1.dtype
'OUT: dtype('float64')'
```



## 배열의 연산

```python
#단순 연산
arr1 = np.array([10,20,30,40])
arr2 = np.array([1,2,3,4])

arr1 + arr2
'OUT: array([11,22,33,44])'

arr1 - arr2
'OUT: array([9,18,27,36])'

arr2 * 2
'OUT: array([2,4,6,8])'

arr2 ** 2
'OUT: array([1,4,9,16], dtype=int(32))'

arr1 * arr2
'OUT: array([10,40,60,160])'

arr1 / arr2
'OUT: array([10., 10., 10., 10.])'

arr1 > 20
'OUT: array([False, False, True, Ture])'

#통계를 위한 연산
arr = np.arange(5)
arr
'OUT: array([0,1,2,3,4])'

[arr.sum(),arr.mean()]
'OUT: [10,2.0]'

[arr.var(),arr.std()]
'OUT: [1.4142135623730951, 2.0]'

arr4 = np.arange(1,5)
arr4
'OUT: array([1,2,3,4])'

arr4.cumsum() #누적합
'OUT: array([1,3,6,10],dtype=int32)'

arr4.cumprod() #누적곱
'OUT: array([1,2,6,24],dtype=int32)'
```



## 행렬 연산

| 행렬 연산 | 사용 예                          |
| --------- | -------------------------------- |
| 행렬곱    | A.dot(B) or np.dot(A,B)          |
| 전치행렬  | A.transpose() or np.transpose(A) |
| 역행렬    | np.linalg.inv(A)                 |
| 행렬식    | np.linalg.det(A)                 |

