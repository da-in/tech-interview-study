# 힙 정렬(Heap Sort)
힙 정렬은 기본적으로 힙 자료구조를 기반으로 한 정렬방식이다.    
[힙 자료구조가 뭐에요?](링크)

힙 정렬은 불안정 정렬에 속하며, 다음과 같은 과정을 거친다.
1. 최대 힙을 구성
2. 현재 힙 루트는 가장 큰 값이 존재함. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈 하나 줄임
3. 힙의 사이즈가 1보다 크면 위 과정 반복

사진  
사진

### 시간 복잡도
최악, 최선, 평균 모두 nlogn의 시간 복잡도를 가짐.

### 장단점
- 장점    
    - 부가적인 메모리가 필요 없음  
    - 어떠한 입력 데이터에 대해서도 최대 복잡도 O(nlgn)을 보장
- 단점
    - 실제 프로그램에서 실행할 경우 평균적인 계산 속도에서 퀵 정렬보다 늦고 안정되지 못함

**힙 소트가 유용할 때**  
- 가장 크거나 가장 작은 값을 구할 때
    - 최소 힙 or 최대 힙의 루트 값이기 때문에 한번의 힙 구성을 통해 구하는 것이 가능  
- 최대 k 만큼 떨어진 요소들을 정렬할 때
    - 삽입정렬보다 더욱 개선된 결과를 얻어낼 수 있음


### 소스코드
**[JAVA]**  
```java
private void solve() {
    int[] array = { 230, 10, 60, 550, 40, 220, 20 };
 
    heapSort(array);
 
    for (int v : array) {
        System.out.println(v);
    }
}
 
public static void heapify(int array[], int n, int i) {
    int p = i;
    int l = i * 2 + 1;
    int r = i * 2 + 2;
 
    if (l < n && array[p] < array[l]) {
        p = l;
    }
 
    if (r < n && array[p] < array[r]) {
        p = r;
    }
 
    if (i != p) {
        swap(array, p, i);
        heapify(array, n, p);
    }
}
 
public static void heapSort(int[] array) {
    int n = array.length;
 
    // init, max heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(array, n, i);
    }
 
    // for extract max element from heap
    for (int i = n - 1; i > 0; i--) {
        swap(array, 0, i);
        heapify(array, i, 0);
    }
}
 
public static void swap(int[] array, int a, int b) {
    int temp = array[a];
    array[a] = array[b];
    array[b] = temp;
}

```


## 출처
https://rninche01.tistory.com/38  
https://gyoogle.dev/blog/algorithm/Heap%20Sort.html

