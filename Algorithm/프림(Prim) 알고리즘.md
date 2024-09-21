## 프림(Prim) 알고리즘이란?
프림 알고리즘(Prim's Algorithm)은 최소 신장 트리(MST, Minimum Spanning Tree)를 찾기 위한 또 다른 그리디 알고리즘이다.

알고리즘의 기본 아이디어는 시작점에서 출발해 인접한 간선을 선택하며 최소 신장 트리를 점진적으로 확장해가는 방식이다. 프림 알고리즘은 힙(heap)이나 우선순위 큐(priority queue)를 사용하여 효율적으로 최소 가중치의 간선을 선택할 수 있다.
<br></br>
 
#### 시간복잡도
프림 알고리즘의 시간 복잡도는 그래프를 구현하는 방식에 따라 다르다

1. 인접 리스트를 사용하고, 우선순위 큐로 구현:
    * O(ElogV), 여기서 E는 간선의 수, V는 정점의 수
    * 우선순위 큐를 통해 간선 선택을 효율적으로 처리
2. 인접 행렬을 사용:
    * O(V2) 시간이 걸립니다. 정점 수가 많을 경우 비효율적
<br></br>


 
 
#### 프림 알고리즘의 기본 원리

1. 초기화:
    * 하나의 정점을 임의로 선택하여 시작한다.
    * 선택된 정점에 인접한 모든 간선을 후보로 추가하기 위해 우선순위 큐를 사용한다.
2. 계산:
    * 시작 정점에서 출발하여 인접한 간선 중 가중치가 가장 작은 간선을 선택한다.
    * 해당 간선이 연결된 새로운 정점을 방문하며, 그 정점에 연결된 모든 간선을 우선순위 큐에 추가한다.
    * 이미 방문한 정점을 연결하는 간선은 무시하며, 아직 방문하지 않은 정점을 연결하는 최소 가중치의 간선을 선택한다.
    * 위 과정을 트리에 포함되는 간선이 V−1V-1V−1개가 될 때까지 반복한다.
3. 응용:
    * 프림 알고리즘은 최소 비용으로 모든 정점을 연결하는 문제, 네트워크 설계, 도로망 구성 등에 사용된다.
    * 그래프의 모든 노드를 포함하는 트리 구조를 효율적으로 구성할 때 사용된다.
<br></br>


 
#### 예시
```
import heapq

# 프림 알고리즘 구현
def prim(n, edges):
    graph = [[] for _ in range(n)]
    
    # 인접 리스트로 그래프 구성
    for u, v, weight in edges:
        graph[u].append((weight, v))
        graph[v].append((weight, u))

    # 최소 신장 트리 (MST)
    mst = []
    total_weight = 0
    visited = [False] * n
    min_heap = [(0, 0)]  # (가중치, 정점) 초기 정점은 0부터 시작

    while min_heap:
        weight, u = heapq.heappop(min_heap)
        
        if visited[u]:
            continue

        visited[u] = True
        total_weight += weight
        mst.append(u)

        for next_weight, v in graph[u]:
            if not visited[v]:
                heapq.heappush(min_heap, (next_weight, v))

    return total_weight, mst

# 예시 그래프: (정점1, 정점2, 가중치)
edges = [
    (0, 1, 10),
    (0, 2, 6),
    (0, 3, 5),
    (1, 3, 15),
    (2, 3, 4)
]

n = 4  # 정점의 수
total_weight, mst = prim(n, edges)
print("최소 신장 트리의 총 가중치:", total_weight)
print("최소 신장 트리에 포함된 정점:", mst)
```
```
최소 신장 트리의 총 가중치: 19
최소 신장 트리에 포함된 정점: [0, 3, 2, 1]
```
