# 계수 정렬 (Count Sort)

## 기본 개념

- 계수 정렬은 비교연산을 사용하지 않고, 이름 그대로 배열 내에 특정 값이 몇번 등장하는지를 통해 정렬을 수행하는 알고리즘

</br>

## 원리

1. 입력 받은 배열 A의 요소값들의 등장횟수를 저장할 배열 B와 최종적으로 정렬된 값들을 담을 배열 C를 준비
2. 입력 받은 배열에서 값을 하나씩 꺼내 해당 값을 B의 인덱스로 사용해 B의 요소 값 하나 증가
   - `B[A[i]]++`
3. 배열 B가 완성되면 B의 각 요소들을 누적합으로 갱신
   - ` B[i] = B[i] + B[i-1]`
4. A의 가장 뒤에서부터 값을 하나씩 꺼내 해당 값을 B의 인덱스로 사용하고 참조된 B의 값 하나 감소한다.
   - `B[A[i]]--`
5. 감소된 B의 값을 배열 C의 인덱스로 사용해 A에서 꺼낸값을 넣는다. 
   - `C[B[A[i]]] = A[i]`
6. A의 모든 요소에 대해 4, 5번 과정 반복 </br>


**이렇게 글로만 보면 배열 수도 많고, 뭔소리인가 싶다,,,예시를 보자!!**

</br>

## 예시

<img width="500" src="https://user-images.githubusercontent.com/102718303/213235975-50d88e95-e0ce-4fc7-b1ce-e92d2cbde247.png">

- 배열 A을 입력 받고, 배열 B와 C를 준비
  - 이때 B의 크기는 A의 `최대값 +1`의 크기이다. (인덱스로 쓰므로,,)

<img width="500" src="https://user-images.githubusercontent.com/102718303/213236212-78e121da-1916-4239-ab2f-c3500d3832ce.png">

- A를 순회하며 등장하는 값들의 등장 횟수를 배열 B의 저장한다.

<img width="500" src="https://user-images.githubusercontent.com/102718303/213236409-63fd0e89-1f5d-4648-9e0a-455e95aba603.png">

- 1차로 완성된 배열 B를 누적합으로 업데이트한다.

<img width="500" src="https://user-images.githubusercontent.com/102718303/213236635-70c43696-e75f-4494-b9bc-b4e3c5ae99ba.png">

- 배열 A의 맨 뒤에서부터 값을 하나씩 꺼내서 B의 인덱스로 접근 후 하나 감소
  - 배열 B에서 6번 인덱스의 값이 6이다. 이는 배열 A에 6보다 같거나 작은 수가 6개 존재한다는 의미
- 해당 값을 C의 인덱스로 접근후 꺼낸 값 저장

<img width="500" src="https://user-images.githubusercontent.com/102718303/213236844-c52db6f0-0f19-4ab9-891d-e446ee69ea32.png">
<img width="500" src="https://user-images.githubusercontent.com/102718303/213237191-0c1b7869-ed61-41b1-a71a-9826fc526905.png">

- 반복하여 정렬 완성

</br>

## 코드
**\<JAVA\>**

```Java
public class Counting_Sort {
    public static void main(String[] args) {
      int[] array = new int[100]; 	//수열의 원소 : 100개
      int[] counting = new int[101];	//수의 범위 : 0~100
      int[] sorted = new int[100];	//정렬 될 배열

      for(int i=0; i<arr.length; i++) {
	      counting[ arr[i] ]++;
      }

      for(int i=1; i<counting.length; i++) {
	      counting[i] += counting[i-1];
      }

      for (int i = array.length - 1; i >= 0; i--) {
        int value = array[i];
        counting[value]--;
        result[counting[value]] = value;
      }
   }
}
```
</br>

**\<PYTHON\>**  
```Python
def counting(arr):
    m = max(K)
    C = [0] * (m + 1)
    for a in arr:
        C[a] += 1
    for i in range(1, m + 1):
        C[i] += C[i - 1]
    result = [0] * len(arr)
    for a in arr:
        result[C[a] - 1] = a
        C[a] -= 1
    return result
```    
</br>

## 분석
- **장점**은 비교연산을 하지 않기 때문에 빠르다.
- **치명적인 단점**은 카운팅을 위한 배열의 길이가 최대값에 의해 결정된다.
  - 만약 (1, 100000) 두 개의 값만 가지더라도 카운팅 배열의 크기는 100001,,
- **시간복잡도**는 `O(N)` 이다.
  - 데이터의 수보다 배열의 크기가 터무니없이 커지면 비효율적! 

</br>

----
## Referance
- https://8iggy.tistory.com/123
- https://jeonyeohun.tistory.com/103
- https://iseunghan.tistory.com/205

