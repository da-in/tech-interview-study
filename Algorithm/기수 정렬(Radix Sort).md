# 기수 정렬(Radix Sort)

## 기본 개념
- **비교 연산**을 수행하지 않고, 조건이 맞는 상황에서 빠른 정렬 속도를 보장하는 알고리즘
- 데이터의 각 자릿수를 낮은 자리수부터 가장 큰 자리수까지 차례대로 올라가며 정렬
- 기수만큼의 추가적인 버킷 저장공간이 필요하다

</br>

## 원리

1. 현재 데이터들 중 가장 큰 자릿수를 파악한다.
2. 각 데이터들의 1의 자리를 비교해서 오름차순으로 정렬한다.
3. 그 다음 10의 자릿수를 오름차순으로 정렬한다.
4. 3번 과정에서 만약 10의 자리가 없다면 0으로 간주하여 가장 앞으로 보낸다. 
5. 위의 과정을 가장 큰 자릿수까지 반복한다.

</br>

## 예시
<img width="600" src="https://user-images.githubusercontent.com/102718303/212923011-3168738c-5bf6-402e-b157-64eb1d12d663.png">

- 현재 데이터들 중 가장 큰 자릿수는 100 자릿수이다. </br>

<img width="600" src="https://user-images.githubusercontent.com/102718303/212923182-ebd71f51-00c5-4e3b-ae32-b75e4efbcb37.png">

- 1의 자릿수부터 비교하여 버켓에 오름차순으로 정렬한다.
- 만약 동일 자릿수가 존재한다면 원래 배열에 담긴 순으로 정렬한다. </br>
<img width="600" src="https://user-images.githubusercontent.com/102718303/212923282-8713c9f2-9712-40b0-a423-7695e84c14d7.png">

- 10의 자릿수를 기준으로 비교하여 오름차순으로 정렬한다.
- 만약 10의 자릿수가 없다면 가장 앞으로 옮기고, 원래있던 데이터의 뒤에 추가한다. </br>

<img width="600" src = "https://user-images.githubusercontent.com/102718303/212923376-f9048ee1-8853-49e8-969a-4573c003c54d.png">

- 마지막으로 100의 자리수을 기준으로 정렬하면 정렬된 배열을 얻을 수 있다.

</br>


## 코드
```Java
import java.util.LinkedList;
import java.util.Queue;

public class RadixBasic {
    // 10진수 기준으로 구현
    private static int BUCKET_NUM = 10;

    public static void sort(int[] arr) {
        // 10진수 버킷 생성
        Queue<Integer>[] bucket = new LinkedList[BUCKET_NUM];
        for(int i=0; i<BUCKET_NUM; i++) {
            bucket[i] = new LinkedList<>();
        }

        int maxLen = maxDigitCount(arr);
        // 각 자리수의 숫자 저장
        int digitNumber = 0;
        // 배열에 다시 저장할 때 필요한 변수
        int arrIndex = 0;

        // 자리수만큼 반복
        for(int i=0; i<maxLen; i++) {
            // 데이터의 개수만큼 반복
            for(int j=0; j<arr.length; j++) {
                digitNumber = getDigit(arr[j], i);
                bucket[digitNumber].add(arr[j]);
            }

            // 버킷에 들어간 데이터를 순서대로 꺼내 배열에 덮어씌우기
            for(int j=0; j<BUCKET_NUM; j++) {
                while (!bucket[j].isEmpty()) {
                    arr[arrIndex++] = bucket[j].remove();
                }
            }
            arrIndex = 0;
        }
    }

    // 숫자의 자리수 반환
    // getDigit(123, 0) => 3
    private static int getDigit(int num, int index) {
        return (int)Math.floor(Math.abs(num) / Math.pow(10, index)) % 10;
    }

    // 숫자의 자리수 구하기
    // digitCount(10) => 2
    private static int digitCount(int num) {
        if (num == 0) {
            return 1;
        }
        // log10을 하면 자리수가 나온다.
        return (int)Math.floor(Math.log10(Math.abs(num))) + 1;
    }

    // 데이터들 중 가장 큰 자리수 반환
    private static int maxDigitCount(int[] arr) {
        int max = 0;

        for(int i=0; i<arr.length; i++) {
            max = Math.max(max, digitCount(arr[i]));
        }
        return max;
    }
}
```

## 알고리즘 분석
- 시간복잡도는 `O(dN)`이다. (N : 데이터의 개수, d는 최대 자리수)

</br>

## 장점
- 자리수를 비교해서 정렬하는 방식이기에 문자열, 정수 정렬이 가능하다.
- 같은 두 수가 있어도 순서가 섞이지 않는 **안정 정렬**이다.
- 속도가 빠르다.

</br>

## 점
- 자리수가 없는 것은 정렬할 수가 없다. (소수 불가,,)
- 중간 결과를 저장하는 **버켓 공간**이 필요하다.
- 버킷의 크기를 모든 케이스에 딱 맞게 정의하기 어렵다. 

</br>

----
## Referance
- https://m.blog.naver.com/adamdoha/222015268529
- https://jeonyeohun.tistory.com/105
- https://sorjfkrh5078.tistory.com/21
- https://banjjak1.tistory.com/52
