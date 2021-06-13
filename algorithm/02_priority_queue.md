# priority queue

* 우선순위 큐 : 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조



## 힙(heap) : 완전 이진트리 자료구조의 일종

* 힙에서는 항상 루트노드를 제거한다
* 최소 힙 : 루트노드가 가장 작은 값을 가짐. 따라서 값이 작은 데이터가 우선적으로 제거됨
* 최대 힙 : 루트노드가 가장 큰 값을 가짐. 따라서 값이 큰 데이터가 우선적으로 제거됨

* min-heapify()
* (상향식)부모노드로 거슬러 올라가며, 부모보다 자신의 값이 더 작은 경우에 위치를 교체
* O(lonN)의 시간복잡도를 가짐



### python 코드

```python
import sys
import heapq

input = sys.stdin.readline

def heapsort(iterable):
    h = []
    result = []
    #모든 원소를 차례대로 삽입
    for value in iterable:
        heapq.heappush(h, value)
    #힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

n = int(input())
arr = []

for i in range(n):
    arr.append(int(input()))

res = heapsort(arr)

for i in range(n):
    print(res[i])
```



참고 코드 : PythonStudy/00_SideStudy/01_Algorithm/02_priority_queue.py
