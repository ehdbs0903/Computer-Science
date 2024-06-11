## 브루트포스(Bruteforce) 알고리즘이란?
가장 단순하지만, 최적의 해를 보장하는 접근법이다.
알고리즘의 기본 아이디어는 모든 가능한 경우의 수를 탐색하여 문제의 해를 찾는 것이다.
<br></br>


#### 시간복잡도
브루트포스 알고리즘의 시간복잡도는 문제의 크기와 경우의 수에 따라 달라진다.
일반적으로 매우 높은 시간복잡도를 가지며, 이는 문제가 커질수록 기하급수적으로 증가한다.

1. 순열 생성:
   
    * n개의 원소에 대한 모든 순열을 생성하는 경우
    * 시간복잡도는 O(n!)이다.
3. 부분집합 생성:
   
    * n개의 원소에 대한 모든 부분집합을 생성하는 경우
    * 시간복잡도는 O(2^n)이다.
5. 문자열 패턴 매칭:
   
    * 텍스트 길이가 n이고, 패턴 길이가 m인 경우, 모든 위치에서 패턴을 비교하는 방식
    * 시간복잡도는 O(n * m)이다.
<br></br>


#### 브루트포스의 기본 원리
1. 가능한 모든 경우 생성:
   
    * 문제를 해결하기 위해 가능한 모든 경우를 생성한다.
3. 각 경우 확인:
   
    * 생성된 각 경우를 평가하여 조건에 맞는지를 확인한다.
5. 최적 해 선택:
   
    * 조건을 만족하는 경우 중 최적의 해를 선택하거나, 모든 경우를 평가한 후 최적의 해를 반환한다.
 <br></br>

 

#### 예시
1. 숫자 찾기:

    * 주어진 배열에서 특정 숫자를 찾는 가장 단순한 방법은 모든 요소를 확인하는 것이다.
```
def find_number(arr, target):
    for num in arr:
        if num == target:
            return True
    return False
```

2. 여행 외판원 문제 (TSP):

    * 모든 경로를 계산하여 최단 경로를 찾는 방식으로, 모든 경로의 순열을 생성하고 평가한다.
```
import itertools

def tsp_bruteforce(graph):
    n = len(graph)
    min_path = float('inf')
    for perm in itertools.permutations(range(n)):
        current_path = sum(graph[perm[i]][perm[i + 1]] for i in range(n - 1))
        current_path += graph[perm[-1]][perm[0]]
        min_path = min(min_path, current_path)
    return min_path
```
