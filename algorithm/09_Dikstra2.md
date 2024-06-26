# 우선순위 큐를 활용한 다익스트라 알고리즘

* 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조



## 힙(Heap)

* 우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나
* 최소 힙과 최대 힙이 있음



### 힙 라이브러리 사용 예제 : 최소 힙

```python
import heapq

#오름차순 힙 정렬
def heapsort(iterable):
    h = []
    result =[]
    #모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    #힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
print(result)
```



### 힙 라이브러리 사용 예제 : 최대 힙

```python
import heapq

#내림차순 힙 정렬
def heapsort(iterable):
    h = []
    result =[]
    #모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    #힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(-heapq.heappop(h))
    return result
```



## 다익스트라 알고리즘 : 개선된 구현 방법

* 단계마다 <u>방문하지 않은 노드중에서 최단 거리가 가장 짧은 노드를 선택</u>하기 위해 **힙(Heap)** 자료 구조를 이용
* 다익스트라 알고리즘이 동작하는 **기본원리는 동일**
  * 현재 가장 가까운 노드를 저장해 놓기 위해 힙 자료구조를 추가적으로 이용한다는 점이 다름
  * 현재의 최단 거리가 가장 짧은 노드를 선택해야 하므로 최소 힙을 사용



###  Python 코드

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) #무한을 의미하는 값으로 10억을 설정

#노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
#시작노드 번호를 입력받기
start = int(input())
#각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
#최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

#모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int,input().split())
    #a번 노드에서 b번 노드로 가능 비용이 c라는 의미
    graph[a].append((b,c))
    
def dikstra(start):
    q = []
    #시작 노드로 가기 위한 최단 거리는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: #큐가 비어있찌 않다면
        #가장 최단거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappush(q)
        #현재 노드가 이미 처리된 적이 잇는 노드라면 무시
        if distance[now] < dist:
            continue
        #현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            #현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
                
#다익스트라 알고리즘을 수행
dikstra(start)

#모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    #도달할 수 없는 경우, 무한이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    #도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```



참고 코드 : PythonStudy/00_SideStudy/01_Algorithm/12_Dikstra.py

참고 코드 : PythonStudy/00_SideStudy/01_Algorithm/12_Dikstra2.py
