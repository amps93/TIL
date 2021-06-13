# 유용한 표준 라이브러리

* 내장 함수 : 기본 입출력 함수부터 정렬함수까지 기본적인 함수들을 제공
  * 파이썬 프로그램을 작성할 때 없어서는 안되는 필수적인 기능을 포함
* itertools : 파이썬에서 반복되는 형태의 데이터를 처리하기 위한 유용한 기능들을 제공
  * 특히 순열과 조합 라이브러리는 코딩 테스트에서 자주 사용됨
* heapq: 힙 자료구조 제공
  * 일반적으로 우선순위 큐 기능을 구현하기 위해 사용
* bisect : 이진 탐색 기능을 제공
* collections : 덱(deque), 카운터(Counter) 등의 유용한 자료구조를 포함
* math : 필수적인 수학적 기능 제공
  * 팩토리얼, 제곱근, 최대공약수, 삼각함수 관련 함수부터 파이와 같은 상수를 포함

```python
#sum
result = sum([1,2,3,4,5])
print(sum)

#min(),max()
min_result = min(7,3,5,2)
max_result = max(7,3,5,2)

#eval()
result = eval("(3+5)*7")
print(result)

#sorted()
result = sorted([9,1,8,5,4])
reverse_result = sorted([9,1,8,5,4],reverse=True)
print(result)
print(reverse_result)

#sorted() with key
array = [('홍길동', 35),('이순신', 75),('아무개',50)]
result = sorted(array, key = lambda x: x[1], reverse = True)
print(result)
```



## 순열과 조합

* 순열 : 서로 다른 n개에서 서로 다른 r개를 선택하여 일렬로 나열하는 것
  * {'A','B','C'}에서 세개를 선택하여 나열하는 경우 : 'ABC','ACB','BAC','BCA','CAB','CBA'
* 조합 : 서로 다른 n개에서 순서에 상관없이 서로 다른 r개를 선택하는것
  * {'A','B','C'}에서 순서를 고려하지 않고 두개를 뽑는 경우 : 'AB','AC','BC'

$$
순열의 수 : nPr = n*(n-1)*(n-2)* \cdots *(n-r-1)
$$

$$
조합의 수 : {nCr = n*(n-1)*(n-2)* \cdots *(n-r-1)\over1}
$$

```python
#순열
from itertools import import permutations

data = ['A', 'B', 'C'] #데이터 준비

result = list(permutations(data, 3)) #모든 순열 구하기
print(result)

#중복 순열
data = ['A', 'B', 'C'] #데이터 준비

result = list(product(data, report=2)) #2개를 뽑는 모든 순열 구하기(중복 허용)
print(result)

#중복 조합
data = ['A', 'B', 'C'] #데이터 준비

result = list(combinations_with_replacment(data, 2)) #2개를 뽑는 모든 조합 구하기(중복 허용)
print(result)
```



## Counter

* Counter는 등장 횟수를 세는 기능을 제공
* 리스트와 같은 반복 가능한 객체가 주어졌을 때 내부의 원소가 몇번씩 등장했는지를 알려줌

```python
from collections import Counter

counter = Counter(['red','bule','red','green','blue','blue'])

print(counter('blue'))
print(counter('green'))
print(dict(counter)) #사전 자료형으로 반환
```



## 최대 공약수와 최소 공배수

* 최대 공약수를 구할때는 math라이브러리의 gcd()함수 사용

```python
import math
#최소 공배수를 구하는 함수
def lcm(a, b):
    return a*b //math.gcd(a,b)

a = 21
b = 14

print(math.gcd(21, 14)) #최대 공약수 계산
print(lcm(21, 14)) #최소 공배수 계산
```



