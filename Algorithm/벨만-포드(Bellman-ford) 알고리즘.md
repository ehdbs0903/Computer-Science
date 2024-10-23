## 벨만-포드(Bellman-ford) 알고리즘이란?
벨만-포드 알고리즘은 최단 경로 알고리즘 중 하나로, 그래프 내의 모든 정점에서 특정 시작 정점까지의 최단 경로를 찾는 알고리즘이다.
특히, 음수 가중치를 가진 간선이 있는 그래프에서도 작동하며, 음수 사이클을 감지할 수 있다.
<br></br>

 
#### 시간복잡도
벨만-포드 알고리즘의 시간 복잡도는 O(V * E)이다. 여기서 V는 정점의 수, E는 간선의 수를 의미한다.
이 시간 복잡도는 모든 간선에 대해 V−1번의 반복을 수행하는 것에서 비롯된다.
<br></br>

 
#### 벨만-포드 알고리즘의 기본 원리

1. 초기화:
    * 시작 정점을 제외한 모든 정점까지의 거리를 무한대(∞)로 설정
    * 시작 정점의 거리는 0으로 설정
2. 계산:
    * 그래프의 모든 간선에 대해 정점을 반복적으로 탐색
    * 각 간선을 검사하여, 해당 간선을 통해 더 짧은 경로가 존재하면 그 경로로 거리를 갱신
    * 이 과정을 정점 수 V−1번 반복. V−1번을 넘어서도 경로가 갱신되면, 음수 가중치 사이클이 존재하는 것을 의미
<br></br>

 
#### 예시
```
# 벨만-포드 알고리즘 구현
def bellman_ford(n, edges, start):
    # 시작 정점에서 모든 정점까지의 거리 배열
    distance = [float('inf')] * n
    distance[start] = 0

    # 정점 수 - 1 번 반복
    for _ in range(n - 1):
        for u, v, weight in edges:
            if distance[u] != float('inf') and distance[u] + weight < distance[v]:
                distance[v] = distance[u] + weight

    # 음수 사이클 탐지
    for u, v, weight in edges:
        if distance[u] != float('inf') and distance[u] + weight < distance[v]:
            print("음수 사이클이 존재합니다.")
            return None

    return distance

# 예시 그래프: (정점1, 정점2, 가중치)
edges = [
    (0, 1, -1),
    (0, 2, 4),
    (1, 2, 3),
    (1, 3, 2),
    (1, 4, 2),
    (3, 2, 5),
    (3, 1, 1),
    (4, 3, -3)
]

n = 5  # 정점의 수
start = 0  # 시작 정점
distance = bellman_ford(n, edges, start)

if distance:
    print("최단 거리:", distance)


# 출력
최단 거리: [0, -1, 2, -2, 1]
```
