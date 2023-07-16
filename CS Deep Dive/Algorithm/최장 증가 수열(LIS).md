# 최장 증가 수열(LIS, Longest Increasing Subsequence)

## 개념
- 원소가 N개인 배열의 일부 원소를 골라 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고, 그 길이가 최대인 부분 수열을 최장 증가 수열이라고 한다.
- 예를 들어 `[6, 2, 5, 1, 7, 4, 8, 3]` 배열의 경우 `[2, 5]`, `[2, 7]`등 증가 수열은 많지만 **최장 증가 수열**은 `[2, 5, 7, 8]`이다.

</br>

## 최장 증가 수열을 구하는 방법

## DP 이용

- DP의 특징은 앞에서의 결과를 재사용 하는 것이다. 
- 따라서 특정 인덱스의 수 k의 앞 순서에 있는 모든 원소들 중 값이 k보다 작은 원소에 대해, 그 각각의 원소에서 끝나는 최장 증가 수열의 길이를 안다면 k에서 끝나는 최장 증가 수열 길이도 구할 수 있다.

<img width="600" src="https://user-images.githubusercontent.com/102718303/214570385-1fe7f29a-02be-402f-8771-67cc29f57b96.png">

- 8 이전의 `[1, 5, 4, 2, 3]`까지의 수열 중 각각의 원소에서 끝나는 최장 증가 수열을 구해보면
  - 1에서 끝나는 LIS 길이 : 1
  - 5에서 끝나는 LIS 길이 : 2 ( [1, 5] )
  - 4에서 끝나는 LIS 길이 : 2 ( [1, 4] )
  - 2에서 끝나는 LIS 길이 : 2 ( [1, 2] )
  - 3에서 끝나는 LIS 길이 : 3 ( [1, 2, 3] )
- 여기서 가장 긴 `[1, 2, 3]`에 현재 수 8을 더한 `[1, 2, 3, 8]`이 8에서 끝나는 최장 증가 수열이다.

### 코드
**[Python]**
```Python
arr = [5, 2, 1, 4, 3, 5]
dp = [1 for _ in range(len(arr))]   // 모든 인덱스의 값을 1로 초기화

for i in range(1, len(arr)):
  for j in range(i) :
    if arr[i] > arr[j]:
       dp[i] = max(dp[i], dp[j] + 1)
       
result = max(dp)
print(result)
```
</br>

### 단점
- 시간 복잡도가 `O(N^2)`,,,

</br>

## 이분 탐색 이용
- DP의 시간 복잡도를 개선한 방법안 이분 탐색을 이용해보자.
- `LIS`를 기록하는 배열을 하나 더 두고, 원래 수열에서 각 원소에 대해 기록하는 배열 내에서의 위치를 찾는다.

<img width="500" src="https://user-images.githubusercontent.com/102718303/214570213-eb9f8e97-4628-4732-a235-8c282cf33f68.png">


### 코드
**[Python]**
```Python
import bisect

arr = [5, 2, 1, 4, 3, 5]
dp = [arr[0]]  // 입력한 배열의 첫번째 원소값으로 초기화
x= len(arr)

for i in range(x):
  if arr[i] > dp[-1]:
     dp.append(arr[i])
  else:
     idx = bisect.bisect_left(dp, arr[i])   // dp가 정렬되어 있다는 가정하에 들어갈 위치 반환
     dp[idx] = arr[i]
     
print(len(dp))     

```
</br>

### 장점
- 시간 복잡도가 `O(NlogN)`이다.

</br>

----
## Referance
- https://chanhuiseok.github.io/posts/algo-49/
- https://4legs-study.tistory.com/106
- https://seohyun0120.tistory.com/entry/%EA%B0%80%EC%9E%A5-%EA%B8%B4-%EC%A6%9D%EA%B0%80%ED%95%98%EB%8A%94-%EB%B6%80%EB%B6%84-%EC%88%98%EC%97%B4LIS-%EC%99%84%EC%A0%84-%EC%A0%95%EB%B3%B5-%EB%B0%B1%EC%A4%80-%ED%8C%8C%EC%9D%B4%EC%8D%AC
- https://one10004.tistory.com/217
