## 크루스칼(Kruskal) 알고리즘이란?
최소 신장 트리(MST, Minimum Spanning Tree) 를  찾기 위한 대표적인 그리디 알고리즘 중 하나이다.

알고리즘의 기본 아이디어는 간선을 가중치 순으로 정렬한 후, 가장 작은 가중치의 간선을 하나씩 선택하면서, 선택된 간선이 사이클을 이루지 않는 경우에만 최소 신장 트리에 포함하는 것이다.
<br></br>

 
#### 시간복잡도
크루스칼 알고리즘의 시간 복잡도는 O(Elog⁡E)이다. 여기서 E는 그래프의 간선 수를 의미한다. 주요 연산은 다음과 같다:

    * 간선 정렬: 간선들을 가중치 순으로 정렬하는 데 O(Elog⁡E)의 시간이 소요된다.
    * 유니온-파인드 연산: 각 간선에 대해 유니온-파인드를 사용하여 사이클을 판별하는 데 O(Eα(V))의 시간이 소요된다. α(V)는 아커만 함수의 역함수로 거의 상수 시간에 가깝다.

따라서 크루스칼 알고리즘의 전체 시간 복잡도는 O(Elog⁡E)이다.
<br></br>


#### 크루스칼 알고리즘의 기본 원리

1. 초기화:
    * 그래프의 모든 간선을 가중치 순으로 정렬한다.
    * 각 정점이 독립적인 집합을 형성하도록 유니온-파인드 자료구조를 초기화한다.
2. 계산:
    * 가중치가 작은 간선부터 하나씩 선택한다.
    * 선택한 간선이 사이클을 만들지 않는다면, 해당 간선을 최소 신장 트리에 포함한다.
    * 유니온-파인드 자료구조를 사용하여 두 정점이 같은 집합에 속해 있는지 확인하고, 다른 집합에 속해 있을 경우 두 집합을 합친다.
    * 모든 정점이 연결될 때까지(또는 V−1개의 간선이 선택될 때까지) 이 과정을 반복한다.
3. 응용:
    * 네트워크 연결 문제, 도로망 설계 등에서 최소 비용으로 모든 노드를 연결해야 하는 경우에 적용된다
    * 사이클 검출, 그래프의 연결성 확인과 같은 문제에도 활용될 수 있다.
<br></br>


#### 예시
```
# 유니온-파인드(Union-Find) 자료구조
class UnionFind:
    def __init__(self, size):
        self.parent = [i for i in range(size)]
        self.rank = [1] * size

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)

        if rootX != rootY:
            if self.rank[rootX] > self.rank[rootY]:
                self.parent[rootY] = rootX
            elif self.rank[rootX] < self.rank[rootY]:
                self.parent[rootX] = rootY
            else:
                self.parent[rootY] = rootX
                self.rank[rootX] += 1

# 크루스칼 알고리즘 구현
def kruskal(n, edges):
    edges.sort(key=lambda x: x[2])  # 간선을 가중치 순으로 정렬
    uf = UnionFind(n)
    mst = []
    total_weight = 0

    for u, v, weight in edges:
        if uf.find(u) != uf.find(v):
            uf.union(u, v)
            mst.append((u, v, weight))
            total_weight += weight

    return mst, total_weight

# 예시 그래프: (정점1, 정점2, 가중치)
edges = [
    (0, 1, 10),
    (0, 2, 6),
    (0, 3, 5),
    (1, 3, 15),
    (2, 3, 4)
]

n = 4  # 정점의 수
mst, total_weight = kruskal(n, edges)
print("최소 신장 트리:", mst)
print("총 가중치:", total_weight)
```
```
최소 신장 트리: [(2, 3, 4), (0, 3, 5), (0, 1, 10)]
총 가중치: 19
```
