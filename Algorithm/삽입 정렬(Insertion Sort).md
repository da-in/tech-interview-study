# 삽입 정렬(Insertion Sort)
**삽입 정렬** 은 두 번째 원소부터 시작하여 그 앞의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는 알고리즘이다.


![image](https://raw.githubusercontent.com/GimunLee/tech-refrigerator/master/Algorithm/resources/insertion-sort-001.gif)

### **시간 복잡도** 

**최악** 의 경우(역으로 정렬되어 있을 경우) 선택정렬과 마찬가지로, (n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2 즉, O(n^2) 이다.

모두 정렬이 되어있는 경우(Optimal)한 경우, 한번씩 밖에 비교를 안하므로 O(n) 의 시간복잡도를 가지게 된다.  
또한, 이미 정렬되어 있는 배열에 자료를 하나씩 삽입/제거하는 경우에는, 현실적으로 최고의 정렬 알고리즘이 되는데, 탐색을 제외한 오버헤드가 매우 적기 때문이다.

최선의 경우는 **O(n)** 의 시간복잡도를 갖고, 평균과 최악의 경우 **O(n^2)** 의 시간복잡도를 갖게 된다.


### **공간 복잡도** 
주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 O(n) 이다.

### **장점** 
- 알고리즘이 단순하다.

- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.

- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. => 제자리 정렬(in-place sorting)

- 안정 정렬(Stable Sort) 이다.

- 선택정렬과 같은 O(n^2) 알고리즘에 비교해서 상대적으로 빠르다.

### **단점** 

- 최악, 평균일때 시간복잡도가 O(n^2)으로, 비효율적이다.

- 길이가 길어질수록 비효율적이다.

### **구현 코드** 

**[javascript]**  
```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let currentVal = arr[i];
    let j;
    for (j = i - 1; j >= 0 && arr[j] > currentVal; j--) {
      arr[j + 1] = arr[j];
    }
    arr[j + 1] = currentVal;
  }
  return arr;
}

console.log(insertionSort([4, 3, 2, 1, 5, -5, 20, 17]));
```
**[JAVA]**  
```java
public class Insertion_Sort {
 
	public static void insertion_sort(int[] a) {
		insertion_sort(a, a.length);
	}
	
	private static void insertion_sort(int[] a, int size) {
		
		
		for(int i = 1; i < size; i++) {
			// 타겟 넘버
			int target = a[i];
			
			int j = i - 1;
			
			// 타겟이 이전 원소보다 크기 전 까지 반복
			while(j >= 0 && target < a[j]) {
				a[j + 1] = a[j];	// 이전 원소를 한 칸씩 뒤로 미룬다.
				j--;
			}
			
			/*
			 * 위 반복문에서 탈출 하는 경우 앞의 원소가 타겟보다 작다는 의미이므로
			 * 타겟 원소는 j번째 원소 뒤에 와야한다.
			 * 그러므로 타겟은 j + 1 에 위치하게 된다.
			 */
			a[j + 1] = target;	
		}
		
	}
}
```