## 분할 정복(Divide and Conquer) 알고리즘이란?
하위 문제들이 중복되지 않을 경우에 사용하는 알고리즘이다.

알고리즘의 기본 아이디어는 복잡한 문제를 더 작고 다루기 쉬운 하위 문제로 나누고, 각각을 독립적으로 해결한 다음, 그 해결 결과를 합쳐 전체 문제의 최적 해를 도출하는 것입니다.
<br></br>


#### 시간복잡도
분할 정복(Divide and Conquer) 알고리즘의 시간복잡도는 문제를 어떻게 분할하고 정복하는지에 따라 달라진다. 일반적인 계산을 위해 사용되는 방법은 재귀식을 통해 시간복잡도를 표현하는 것이다. 이는 문제의 크기를 줄여가면서 하위 문제의 수와 각 하위 문제를 해결하는 데 걸리는 시간을 고려한다.

1. 이진 탐색(Binary Search):
    * 분할: 배열을 반으로 나눔.
    * 정복: 한 쪽 반을 선택하여 탐색을 계속함.
    * 결합: 추가적인 결합 작업은 없음.
    * T(n)=O(logn).
2. 합병 정렬(Merge Sort):
    * 분할: 배열을 두 개의 동일한 크기의 하위 배열로 나눔.
    * 정복: 각 하위 배열을 재귀적으로 정렬.
    * 결합: 두 정렬된 하위 배열을 합병.
    * T(n)=O(nlogn).
3. 퀵 정렬(Quick Sort):
    * 분할: 피벗을 기준으로 배열을 두 부분으로 나눔.
    * 정복: 각 부분을 재귀적으로 정렬.
    * 결합: 추가적인 결합 작업은 없음.
    * 최악의 경우 T(n)=O(n^2), 평균적으로O(nlogn).
<br></br>
 

#### 분할 정복의 기본 원리
1. 분할(Divide):
    * 주어진 문제를 두 개 이상의 작은 문제로 나눈다.
2. 정복(Conquer):
    * 각 하위 문제를 재귀적으로 해결한다. 하위 문제가 충분히 작아질 경우, 직접 해결할 수 있다.
3. 결합(Combine):
    * 정복된 하위 문제의 해결책을 조합하여 원래 문제의 해결책을 얻는다.
<br></br>

#### 예시
1. 이진 탐색 (Binary Search)
    * 주어진 정렬된 배열에서 특정 값의 위치를 찾는 알고리즘
    * 배열을 반으로 나누고 타겟 값이 중앙값보다 큰지 작은지를 비교하여 해당 부분 배열에서만 탐색을 계속한다.
```
def binary_search(arr, left, right, target):
    if right >= left:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] > target:
            return binary_search(arr, left, mid - 1, target)
        else:
            return binary_search(arr, mid + 1, right, target)
    return -1
```

2. 머지 소트 (Merge Sort):
    * 배열을 반으로 나누고, 각 부분을 정렬한 다음, 두 정렬된 리스트를 하나의 정렬된 리스트로 병합한다.
```
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]

        merge_sort(L)
        merge_sort(R)

        i = j = k = 0
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1

        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1

        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
```
