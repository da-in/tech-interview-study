# 레드-블랙트리(Red-Black Tree)

## 개념
- 레드-블랙 트리는 빨간색 노드와 검은색 노드로 이루어진 자가 균형 이진 탐색 트리이다.

## 조건

- 모든 노드는 **빨간색** 혹은 **검은색**이다.
- 루트 노드는 검은색
- 모든 리프 노드는 검은색
- 빨간색 노드의 자식은 검은색 -> 빨간색 노드가 연속으로 나올 수 없다.
- 모든 리프노드에서 **Black Depth**는 같다

<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcitWfI%2FbtrptgRQlFi%2Fvd9FwY1WQKUpKDkjZWIGD1%2Fimg.png">

\**NIL 노드는 값이 없는 특수한 노드이고, 레드-블랙 트리에서 리프 노드에 해당한다. 또한 모두 검은색이다.*

</br>

뭔말이여,,레드-블랙 트리는 예시를 보는게 좋다!

## 예시

## 레드-블랙 트리 삽입 과정
- 먼저 부모노드를 **P**, 조상 노드를 **G**, 삽입 노드를 **N**, 삼촌 노드(부모의 형제)를 **U**라고 하자.
- 레드-블랙 트리의 삽입 노드는 반드시 **빨간색**이다.

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYG3yV%2FbtrpoxGRp6g%2FfBAd1VvrqdWy6QRRSKTX3k%2Fimg.png">

- 만약 예시처럼 `3`을 삽입하는 경우 연속으로 빨간색 노드가 등장하므로 조건에 위배된다.
- 두 가지 방법으로 해결한다.

### 1. Restructuring
- Restructuring은 U노드가 검은색일 때 수행한다.
- 수행과정은 예시로 먼저 보면

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqszUV%2Fbtrpdq9Hhyf%2FHgbBFX55xi67E3JkjPpx7K%2Fimg.png">

- 먼저 N노드와, P노드, G노드를 오름차순으로 정렬한다. -> 삽입한 N노드 값이 중간 값이 된다.

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAUx5F%2FbtrppAcjYXR%2FczbUJZ1GU22ufSGewtyYQ1%2Fimg.png">

- 중간 값인 `3`을 부모 노드로 설정하고, 나머지 `2`와 `5`를 자식 노드로 설정한다.

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMASjd%2Fbtrpq6WhqWJ%2F6Vg1qcMarQEqQDk1oKGi51%2Fimg.png">

- 이후 새로운 부모 노드인 `3`을 검은색으로 바꾸고, 나머지 두 자식을 빨간색으로 바꿔주면 된다.

- 정리해보면
  1. N, P, G를 오름차순으로 정렬
  2. 중간 값을 부모로 만들고, 나머지 둘을 자식으로 만든다.
  3. 새로운 부모노드를 검은색으로 만들고, 두 자식을 빨간색으로 만든다. 
                      

### 2. Recoloring
- Recoloring은 U 노드가 빨간색일때 수행한다.
- 수행 과정은 예시를 먼저보면

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvBBus%2FbtrpjwouNiw%2FcBnlbiBxKyKUb8XRBvf4D1%2Fimg.png">

- 먼저 P노드와 U노드를 검은색으로 바꾸고, G노드를 빨간색으로 바꾼다.
- 이후 또 다시 연속 빨간색이 발생하게 된다.
- 해당 케이스가 **Restructuring**인지 **Recoloring**인지 판단 후 수행을 반복하면 된다.

</br>

- 정리해보면
  1. N노드의 P노드와 U노드를 검은색으로 바꾸고, G노드를 빨간색으로 바꾼다.
     1. 만약 G노드가 루트 노드라면 검은색으로 바꾸고 완료
     2. G노드를 빨간색으로 바꾼 후 또 다시 연속 빨간색이 발생하면 두가지 케이스 중 해당하는 방법을 수행한다.


## 레드-블랙 트리 삭제 과정
- 만약 삭제하려는 노드가 **빨간색**이면 그냥 삭제해주면 된다. (연속적인 검은색 노드는 문제 없다!)
- 삭제하려는 노드가 **검은색**인 경우에는 리프노드까지 거치는 **검은색** 노드의 수가 일정해야 하므로 따져봐야 한다. 

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOLLEC%2FbtrLF4ql2R8%2FCp7CD8pe77mE7X1JlDJWh1%2Fimg.png">

- 위의 예시처럼 그냥 삭제해버리면 규칙에 위배된다.

</br>

### Case 1

<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlpQ5b%2FbtrLJpsWNkH%2Fjpk752WzGVg8hAPSYAO6k1%2Fimg.png">

- 해당 케이스는 삭제하려는 노드의 부모가 **빨간색**노드이고, 형제의 자식들이 모두 **검은색**인 경우에 성립한다. 
- 부모의 색과 형제의 색을 바꿔주면 해결된다.

</br>

### Case 2
<img width="300" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtQYyr%2FbtrLJYIaUpR%2FmGROsOKFdZg88z0zv7Nre0%2Fimg.png">

- 해당 케이스는 형제의 조카 중 하나가 **빨간색**노드 이기 때문에 Case 1 처럼 해결할 수 없다. (연속적인 **빨간색** 노드)

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTWkcQ%2FbtrLGktbXJm%2FQLDnIbc7Hh9MtxbWKpK3f0%2Fimg.png">

- 위 예시의 A노드를 기준으로 삭제하려는 노드 방향 회전을 통해 해결할 수 있다.
- 삭제하려는 노드를 삭제해도 규칙에 위배되지 않는다.

</br>

### Case 3
<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb2NVyL%2FbtrLJkkXPwn%2Ff0uxzkjUTjmK2Ze4BBMx90%2Fimg.png">

- 해당 케이스는 형제의 자식 노드 모두 **빨간색**노드인 경우이다.
- Case 2와 같이 회전을 통해 해결 할 수 있다.

<img width="540" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fq7M44%2FbtrLHVfsZTi%2FkXJKZTwrnr9yCbyZtuBKF0%2Fimg.png">

- 회전 후 **삽입 과정**에서의 **Recoloring**을 수행하면 된다.

</br>

## 장점
- 특정 조건을 지키며 균형 이진트리를 만족하기 때문에 탐색, 삽입, 삭제 모두 `O(logN)`의 시간복잡도를 가진다.

----

## Referance

**레드-블랙 시물레이터**
- https://www.cs.usfca.edu/~galles/visualization/RedBlack.html

- https://code-lab1.tistory.com/62
- https://dev-game-standalone.tistory.com/94



