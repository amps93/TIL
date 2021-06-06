# tree (이진탐색트리)

* 이진 탐색 트리 : 이진 탐색이 동작할 수 있도록 고안된 효율적인 탐색이 가능한 자료구조
* 이진 탐색트리의 특징 : 왼쪽자식노드 < 부모노드 < 오른쪽자식노드



## 트리의 순회

* 트리자료구조에 포함된 노드를 특정한 방법으로 한 번씩 방문하는 방법

* 대표적인 트리 순회 방법
  * 전위 순회 : 루트를 먼저 방문
  
  * 중위 순회 : 왼쪽 자식을 방문한 뒤 루트를 방문

  * 후위 순회 : 오른쪽 자식을 방문한 뒤 루트를 방문
  
    ```
         A
        /  \                   전위 순회 : A B D E C F G
      B      C                 중위 순회 : D B E A F C G
     / \    / \                후위 순회 : D E B F G C A
    D   E  F   G
    ```
  
    


### python 코드

```python
class Node:
    def __init__(self, data, left_node, right_node):
        self.data = data
        self.left_node = left_node
        self.right_node = right_node

#전위 순회
def pre_order(node):
    print(node.data, end=' ')
    if node.left_node != None:
        pre_order(tree[node.left_node])
    if node.right_node != None:
        pre_order(tree[node.right_node])

#중위 순회
def in_order(node):
    if node.left_node != None:
        in_order(tree[node.left_node])
    print(node.data, end=' ')
    if node.right_node != None:
        in_order(tree[node.right_node])

#후위 순회
def post_order(node):
    if node.left_node != None:
        post_order(tree[node.left_node])
    if node.right_node != None:
        post_order(tree[node.right_node])
    print(node.data,end=' ')

n = int(input())
tree = {}

for i in range(n):
    data, left_node, right_node = input().split()
    if left_node == "None":
        left_node = None
    if right_node == "None":
        right_node = None
    tree[data] = Node(data, left_node, right_node)

pre_order(tree['A'])
print()
in_order(tree['A'])
print()
post_order(tree['A'])

'''
입력 예시

7
A B C
B D E
C F G
D None None
E None None
F None None
G None None
'''
```
