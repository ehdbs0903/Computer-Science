## 이진 탐색 / 이분 탐색 (Binary Search) 알고리즘이란?
배열에서 특정한 값을 효율적으로 찾기 위한 알고리즘이다.

알고리즘의 기본 아이디어는 탐색 범위를 반으로 줄여가면서 원하는 값을 찾는 것이다. 정렬된 상태의 배열에서만 사용할 수 있다.
<br></br>


#### 시간복잡도
O(log n)
<br></br>


#### 이분 탐색의 기본 원리
1. 초기화:
    * start (시작점)를 배열의 첫 번째 인덱스로, end (끝점)를 배열의 마지막 인덱스로 설정한다.
      
2. 반복 조건:
    * start가 end보다 작거나 같은 동안 반복한다. (start가 end를 초과하면 찾고자 하는 값이 배열에 없다는 것을 의미)
      
3. 중간점 찾기:
    * 배열의 중간 지점 mid를 (start + end) / 2로 계산한다.
      
4. 탐색 로직:
    * 찾고자 하는 값 target과 중간점 mid에 위치한 값을 비교한다.
    * 만약 target이 mid에 위치한 값보다 작으면, end를 mid - 1로 업데이트하여 상위 반을 제외시킨다.
    * 만약 target이 mid에 위치한 값보다 크면, start를 mid + 1로 업데이트하여 하위 반을 제외시킨다.
    * 만약 target이 mid에 위치한 값과 동일하면, mid가 찾고자 하는 값의 위치이므로 탐색을 종료한다.

<br></br>

#### 예시
![image](https://github.com/ehdbs0903/Computer-Science/assets/82309982/584e8122-b629-4f13-a15a-014c6cdc499e)
<br></br>


#### 구현
```
def binary_search(array, target):
    start, end = 0, len(array) - 1

    while start <= end:
        mid = (start + end) // 2
        if array[mid] == target:
            return mid  # 찾은 경우, 인덱스 반환
        elif array[mid] < target:
            start = mid + 1
        else:
            end = mid - 1

    return -1  # 찾지 못한 경우
```
