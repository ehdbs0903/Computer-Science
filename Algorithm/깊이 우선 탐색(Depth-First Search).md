## 깊이 우선 탐색 / DFS (Depth-First Search) 알고리즘이란?
그래프에서 모든 노드를 방문하는 알고리즘 중 하나이다.

알고리즘의 기본 아이디어는 한 방향으로 갈 수 있는 한 최대한 깊게 그래프를 탐색하는 것이다. 
<br></br>


#### 시간복잡도
DFS의 시간 복잡도는 그래프의 표현 방식에 따라 달라진다.

1. 인접 리스트 사용 시:

    * 각 노드에 대해 모든 인접한 노드를 방문해야 한다.
    * 각 노드는 한 번씩 방문하며, 각 노드의 모든 인접한 노드를 확인하는 데 걸리는 시간은 인접한 노드의 개수에 비례한다.
    * 따라서 시간 복잡도는 O(V + E) 이다.  (* V = 정점의 수, E = 간선의 수)
```
{
  'A': ['B', 'C', 'D'],
  'B': ['A'],
  'C': ['A', 'D'],
  'D': ['A', 'C', 'E'],
  'E': ['D']
}
```

2. 인접 행렬 사용 시

    * 어떤 노드에 인접한 노드를 확인하기 위해서는 해당 노드의 모든 이웃을 대상으로 하여 해당하는 행을 전부 확인해야 한다.
    * 각 노드를 방문할 때마다 V번의 검사가 이루어지므로, 총 시간 복잡도는 O(V^2)이다.  (* V = 정점의 수)
```
[
  [0, 1, 1, 1, 0],  # A
  [1, 0, 0, 0, 0],  # B
  [1, 0, 0, 1, 0],  # C
  [1, 0, 1, 0, 1],  # D
  [0, 0, 0, 1, 0]   # E
]
```
<br></br>


#### 깊이 우선 탐색의 기본 원리
1. 시작 노드 설정:
    * 탐색을 시작할 노드(시작 노드)를 선택한다.
2. 방문 처리:
    * 현재 노드를 방문 리스트에 추가하거나, 방문 여부를 나타내는 배열에 체크하며 방문 처리한다. 
3. 인접 노드 탐색:
    * 현재 노드에 인접한 노드 중에서 아직 방문하지 않은 노드를 찾는다.
    * 인접 노드를 찾으면, 그 인접 노드를 방문한다.
4. 되돌아가기:
    * 더 이상 방문할 인접 노드가 없으면 이전 노드로 돌아간다.
5. 탐색 반복:
    * 새로운 현재 노드에서 위 과정을 반복한다.
6. 탐색 종료:
    * 모든 노드를 방문하면 탐색을 종료한다.
<br></br>


#### 예시
![image](https://github.com/ehdbs0903/Computer-Science/assets/82309982/54b935eb-4be1-4b68-8b67-8a94882adbf8)
<br></br>


#### 구현
1. 재귀 함수로 구현
```
def dfs_recursive(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    print(node, end=' ')

    for neighbour in graph[node]:
        if neighbour not in visited:
            dfs_recursive(graph, neighbour, visited)
```

2. 스택으로 구현
```
def dfs_stack(graph, start_node):
    visited = set()
    stack = [start_node]

    while stack:
        node = stack.pop()
        if node not in visited:
            print(node, end=' ')
            visited.add(node)
            # 순서를 유지하기 위해 인접한 노드를 스택에 역순으로 추가.
            stack.extend(reversed(graph[node]))
```
