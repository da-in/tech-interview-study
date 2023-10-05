# 이분 탐색(Binary Search)

- `이분 탐색(Binary Search)` 알고리즘은 정렬되어 있는 리스트에서 탐색 범위를 절반씩 줄여가며 데이터를 탐색하는 방법
- 배열 내부의 데이터가 오름차순으로 정렬되어 있어야만 사용할 수 있다.
- 변수 3개 `start, end, mid` 를 사용하여 탐색한다. 

## 동작 방식
1. 배열의 중간 값을 가져온다.
2. 가져온 중간 값과 검색 값을 비교한다.
   1. 중간 값이 검색 값과 같다면 종료
   2. 중간 값보다 검색 값이 크다면 중간 값을 기준으로 배열의 오른쪽 구간 탐색
   3. 중간 값보다 검색 값이 작다면 중간 값을 기준으로 배열의 왼쪽 구간 탐색
3. 값을 찾거나 간격이 비어 있을 때까지 반복 </br></br>

![이진탐색 애니메이션](https://user-images.githubusercontent.com/102718303/211353741-3bda8bce-da11-41bb-8538-830d1540593d.gif)




## 구현

### 반복문으로 구현
- [JAVA]
```java
public static boolean BSearch(int[] arr, int n) {
  int left = 0;
  int right = arr.length -1;
  int mid;
  
  while (left <= right) {
    mid = (left + right) / 2;
    if(arr[mid] < n) 
      left = mid + 1;
    else if (arr[mid] > n)
      right = mid -1;
    else 
      return true;
  }
  return false;
}
```
- [Python]
```python
def binary_search(arr, n):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] < n:
            left = mid + 1
        elif arr[mid] > n:
            right = mid - 1
        else:
            return True

    return False

```

#### 재귀로 구현 
- [JAVA]
```java
public static boolean BSearch(int[] arr, int n, int left, int right) {
  if(left > right) 
    return false;
    
  int mid = (left + right) / 2;
  
   if(arr[mid] < n) 
      return BSearch(arr, n, mid+1, right);
    else if (arr[mid] > n)
      return Bsearch(arr, n, left, mid -1);
    else 
      return true;
}
```
- [Python]
```python
def binary_search_recursive(arr, n, left, right):
    if left > right:
        return False

    mid = (left + right) // 2

    if arr[mid] < n:
        return binary_search_recursive(arr, n, mid + 1, right)
    elif arr[mid] > n:
        return binary_search_recursive(arr, n, left, mid - 1)
    else:
        return True
```


## 특징
- `O(logN)`의 시간 복잡도를 가진다. -> 단계마다 탐색 범위를 반으로 나누는 것과 동일 </br>

----
## Reference
- https://velog.io/@kimdukbae/%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search
- https://yoongrammer.tistory.com/75
- https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search
