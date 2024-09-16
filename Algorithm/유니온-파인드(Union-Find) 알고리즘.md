## 유니온-파인드(Union-Find) 알고리즘이란? 
유니온-파인드 알고리즘은 서로소 집합(Disjoint Set)을 효율적으로 관리하는 자료구조이다. 주로 그래프에서 사이클을 판별하거나, 네트워크 연결 문제에서 각 노드 간의 연결 여부를 확인하는 데 사용된다.

알고리즘의 기본 아이디어는 여러 개의 원소가 존재하는 집합을 트리 구조로 표현하고, 두 집합을 합치거나(Union) 특정 원소가 속한 집합을 찾는(Find) 연산을 효율적으로 수행하는 것이다.
<br></br>
 
#### 시간복잡도
유니온-파인드 알고리즘의 시간 복잡도는 경로 압축(Path Compression)과 랭크에 의한 합치기(Union by Rank)를 사용할 경우, 거의 상수 시간인 O(α(n))이 된다. 여기서 α(n)은 아커만 함수의 역함수로, 매우 느리게 증가하는 함수이기 때문에 실질적으로 O(1)로 간주할 수 있다.
<br></br>
 
#### 유니온-파인드의 기본 원리
1. 초기화:
    * 각 원소는 초기에는 자신을 부모로 가리키며, 이를 통해 각 원소가 독립적인 집합을 형성한다.
    * 트리의 높이(또는 랭크)를 저장하기 위한 배열을 함께 초기화하여 나중에 두 집합을 합칠 때 최적화에 사용한다.
2. 계산:
    * Find 연산: 특정 원소가 속한 집합의 루트 노드를 찾는다. 경로 압축을 사용하여 탐색하는 과정에서 만나는 모든 노드의 부모를 직접 루트 노드로 바꿔줌으로써 이후의 탐색을 빠르게 만든다.
    * find(x)는 원소 x가 속한 집합의 루트를 찾는 과정이다.
    * Union 연산: 두 집합을 합칠 때, 랭크를 사용하여 트리의 높이가 낮은 쪽을 높은 쪽의 서브트리로 연결한다. 이를 통해 트리의 높이를 최소화하고, find 연산이 더 빠르게 동작할 수 있게 한다.
    * union(x, y)는 두 원소 x와 y가 속한 집합을 하나로 합친다.
3. 응용:
    * 그래프에서 사이클을 판별하는 문제, 최소 신장 트리(MST) 생성, 네트워크 연결 문제 등 다양한 문제에 적용할 수 있다.
    * 주어진 요소들이 같은 집합에 속하는지 여부를 효율적으로 관리할 수 있다.
<br></br>

```
# 유니온-파인드 알고리즘 구현
class UnionFind:
    def __init__(self, size):
        self.parent = [i for i in range(size)]  # 각 원소의 부모를 저장
        self.rank = [1] * size  # 각 집합의 높이(랭크)를 저장

    # find 연산: 경로 압축을 통해 최적화
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # 경로 압축
        return self.parent[x]

    # union 연산: 랭크에 따라 트리의 높이를 최소화하며 합침
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)

        if rootX != rootY:
            # 랭크가 더 높은 쪽을 루트로 함
            if self.rank[rootX] > self.rank[rootY]:
                self.parent[rootY] = rootX
            elif self.rank[rootX] < self.rank[rootY]:
                self.parent[rootX] = rootY
            else:
                self.parent[rootY] = rootX
                self.rank[rootX] += 1

# 예시 사용
uf = UnionFind(5)
uf.union(0, 1)
uf.union(1, 2)
print(uf.find(2))  # 출력: 0, 모든 노드 0, 1, 2는 하나의 집합에 속함
print(uf.find(3))  # 출력: 3, 노드 3은 독립적인 집합에 속함
uf.union(3, 4)
print(uf.find(4))  # 출력: 3, 노드 3과 4는 하나의 집합에 속함
```
