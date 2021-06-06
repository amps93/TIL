# stack&queue



## stack

* 선입후출의 자료구조



### python 코드

```python
#stack : 선입후출
stack = []

stack.append(5)
stack.append(2)
stack.append(3)
stack.append(7)
stack.pop() #7 빠짐
stack.append(1)
stack.append(4)
stack.pop() #4 빠짐

print(stack[::-1]) #최상단 원소부터 출력
print(stack) #순서대로 출력
```



## queue

* 선입선출의 자료구조



### python 코드

```python
#que : 선입선출
from collections import deque

queue = deque()

queue.append(5)
queue.append(2)
queue.append(3)
queue.append(7)
queue.popleft() #5 빠짐
queue.append(1)
queue.append(4)
queue.popleft() #2 빠짐

print(queue) #먼저 들어온 순서대로 출력
queue.reverse() #역순으로 바꾸기
print(queue) #나중에 들어온 원소부터 출력
```