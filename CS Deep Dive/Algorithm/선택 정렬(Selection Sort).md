# 선택 정렬(Selection Sort)
**선택 정렬** 은 첫 번째 자료를 두 번째 자료부터 마지막 자료까지 차례대로 비교하여 가장 작은 값을 찾아 첫 번째에 놓고, 두 번째 자료를 세 번째 자료부터 마지막 자료까지와 차례대로 비교하여 그 중 가장 작은 값을 찾아 두 번째 위치에 놓는 과정을 반복하며 정렬을 수행한다.

1회전을 수행하고 나면 가장 작은 값의 자료가 맨 앞에 오게 되므로 그 다음 회전에서는 두 번째 자료를 가지고 비교한다. 마찬가지로 3회전에서는 세 번째 자료를 정렬한다.

>백문이 불여일견! 어떻게 돌아가는지 눈으로 보자

![image](https://raw.githubusercontent.com/GimunLee/tech-refrigerator/master/Algorithm/resources/selection-sort-001.gif)

### **예제**
| 패스 | 테이블 | 최솟값 |
|---|---|---|
|0|[9,1,6,8,4,0]|0|
|1|[0,**1,6,8,4,9**]|1|
|2|[0,1,**6,8,4,9**]|4|
|3|[0,1,4,**8,6,9**]|6|
|4|[0,1,4,6,**8,9**]|8|


### **시간 복잡도** 

데이터의 개수가 n개라고 했을 때,

- 첫 번째 회전에서의 비교횟수 : 1 ~ (n-1) => n-1

- 두 번째 회전에서의 비교횟수 : 2 ~ (n-1) => n-2

- ...

- (n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2

비교하는 것이 상수 시간에 이루어진다는 가정 아래, n개의 주어진 배열을 정렬하는데 O(n^2) 만큼의 시간이 걸린다.  
최선, 평균, 최악의 경우 시간복잡도는 **O(n^2)** 으로 동일하다.

### **공간 복잡도** 
주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 O(n) 이다.

### **장점** 
- Bubble sort와 마찬가지로 알고리즘이 단순하다.

- 정렬을 위한 비교 횟수는 많지만, Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다.

- Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. => 제자리 정렬(in-place sorting)

### **단점** 

- 시간복잡도가 O(n^2)으로, 비효율적이다.

- 불안정 정렬(Unstable Sort) 이다.

    > **[불안정 정렬이 뭐에요?]**  
안정 정렬 - 동일한 값에 대해 기존의 순서가 유지되는 정렬 방식 *(버블 정렬, 삽입 정렬)*  
불안정 정렬 - 동일한 값에 대해 기존의 순서가 유지되지 않는 정렬 방식 *(선택 정렬)*  
**Array - [B, b, a, c]**  *( a < b < c )*  
b와 B는 같은 수 일 때 *(b == B)* 선택 정렬 시 위의 결과는 아래와 같다.  
**Array - [a, b, B, c]**  
b 와 B는 동일한 수였지만 B가 순서로 보자면 b 보다 앞서 있었다.  
하지만 선택 정렬 후 B가 b보다 뒤로 배치되면서 순서가 바뀌었다.  
이렇게 순서가 유지되지 않는 경우를 불안정 정렬이라함으로써 선택 정렬은 불안정 정렬이 되는 것이다.

### **구현 코드** 

**[javascript]**  
```javascript
function selectionSort (array) {
  for (let i = 0; i < array.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[minIndex] > array[j]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      let swap = array[minIndex];
      array[minIndex] = array[i];
      array[i] = swap;
    }
    console.log(`${i}회전: ${array}`);
  }
  return array;
}
console.log(selectionSort([5, 4, 3, 2, 1]));
```
**[JAVA]**  
```java
public class Selection_Sort {
 
	public static void selection_sort(int[] a) {
		selection_sort(a, a.length);
	}
	
	private static void selection_sort(int[] a, int size) {
		
		for(int i = 0; i < size - 1; i++) {
			int min_index = i;	
			
			// 최솟값을 갖고있는 인덱스 찾기 
			for(int j = i + 1; j < size; j++) {
				if(a[j] < a[min_index]) {
					min_index = j;
				}
			}
			
			// i번째 값과 찾은 최솟값을 서로 교환 
			swap(a, min_index, i);
		}
	}
	
	private static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
	
}
```
**[python]**  
```python
def selectionSort(x):
	length = len(x)
	for i in range(length-1):
	    indexMin = i
		for j in range(i+1, length):
			if x[indexMin] > x[j]:
				indexMin = j
		x[i], x[indexMin] = x[indexMin], x[i]
	return x
```

