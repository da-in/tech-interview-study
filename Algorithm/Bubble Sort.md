# 거품정렬 (Bubble Sort)
2개의 인접한 데이터를 비교해서 앞에 있는 데이터가 뒤에 있는 데이터보다 크면 자리를 바꾸는 정렬 알고리즘

![images_eunseokim_post_17049874-0f11-49fc-bb36-74800f1ea0b0_2518323758FDB83613](https://user-images.githubusercontent.com/50827930/209081597-475d2ffe-f057-4f72-8f5b-07dc9a4b2e09.gif)

위 예시를 보면 큰 요소들이 거품처럼 보글보글 올라와 맨 뒤부터 쌓이는 것을 확인할 수 있다!<br/>
정렬을 1회전 수행할 때마다 가장 큰 자료가 맨 뒤로 이동하며, 이렇게 1회전 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어난다.

## 실습
배열에 7, 4, 5, 1, 3 이 저장되어 있다고 가정하고 자료를 오름차순으로 정렬해보자.

![bubble-sort](https://user-images.githubusercontent.com/50827930/209083731-37ef70de-6437-4ab4-a5e3-c981d370645c.png)

## 코드로 구현하자면 (Javascript 기준)
```javascript
function bubbleSort (array) {
  for (let i = 0; i < array.length; i++) { //자료의 개수만큼 반복(회차)
    let swap = false;
    for (let j = 0; j < array.length - 1 - i; j++) { //한 회차마다 맨 뒤에 정렬에서 제외되는 데이터 제외하고 반복
      if (array[j] > array[j + 1]) { //2개의 인접한 데이터 비교하여 앞에 있는 데이터가 뒤에 있는 데이터보다 크면 자리를 바꾼다
        [array[j], array[j+1]] = [array[j+1], array[j]]
        swap = true;
      }
    }
    if(!swap) break
  }
  return array;
}
```

## 시간 복잡도
- Worst Case : O(n^2) => 정렬이 하나도 안되어 있는 경우
- Best Case : O(n) => 이미 정렬이 되어있는 경우

## 장단점
### 장점
- in place 알고리즘이기 때문에 메모리가 절약된다. (※in place : 자료를 정렬할 때 추가적인 메모리 공간이 필요하지 않음!)
- 구현하기 매우 쉽다....라고 함

### 단점
- 자료의 개수가 많아질 수록 성능이 매우 떨어진다. (최악의 경우 O(n^2)이 소요되기 때문에!)

## Reference 
- https://velog.io/@eunseokim/%EB%B2%84%EB%B8%94-%EC%A0%95%EB%A0%ACbubble-sort
- https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html
- https://im-developer.tistory.com/133
