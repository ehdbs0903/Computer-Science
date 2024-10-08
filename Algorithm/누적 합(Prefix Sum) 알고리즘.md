## 누적 합(Prefix Sum) 알고리즘이란?
주어진 배열에서 각 요소까지의 합을 계산하여 새로운 배열을 생성하는 알고리즘이다. 이는 특정 구간의 합을 빠르게 계산할 때 유용하며, 특히 큰 데이터를 다룰 때 효율적이다.

알고리즘의 기본 아이디어는 원래 배열의 첫 번째 요소부터 마지막 요소까지의 합을 점진적으로 계산하여 새로운 배열에 저장하는 것이다.
<br></br>
 

#### 시간복잡도
누적합 알고리즘의 시간복잡도는 O(n)입니다. 배열의 각 요소에 대해 한 번씩만 계산하면 되기 때문에 매우 효율적이다.

누적합을 통해 구간 합을 계산할 때는 추가적인 반복 없이 O(1) 시간에 계산할 수 있다.
<br></br>
 

#### 누적 합의 기본 원리
1. 초기화:
    * 첫 번째 요소를 그대로 사용하여 누적합 배열의 첫 번째 요소를 초기화
2. 계산:
    * 두 번째 요소부터 마지막 요소까지의 합을 계산하여 누적합 배열에 저장
3. 응용:
    * 누적합 배열을 사용하여 특정 구간의 합이나 다른 통계적 값을 효율적으로 계산
<br></br>


#### 예시
구간 합 계산
  * 주어진 배열에서 각 요소까지의 합을 계산하여 누적합 배열을 생성하고 누적합 배열을 사용하여 특정 구간 [i,j][i, j][i,j]의 합을 계산

```
def prefix_sum(arr):
    n = len(arr)
    pre_sum = [0] * n
    pre_sum[0] = arr[0]
    
    for i in range(1, n):
        pre_sum[i] = pre_sum[i - 1] + arr[i]
        
    return pre_sum
    
    
def range_sum(pre_sum, i, j):
    if i == 0:
        return pre_sum[j]
    else:
        return pre_sum[j] - pre_sum[i - 1]
```
![image](https://github.com/user-attachments/assets/575e9e0f-6cf4-41b3-a168-908d4b4d3f71)

<br></br>
