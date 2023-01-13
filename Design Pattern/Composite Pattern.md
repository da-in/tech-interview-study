# Composite Pattern

**단일 객체**와 그 객체들을 가지는 **집합 객체**를 같은 타입으로 취급하고, 트리 구조로 객체들을 엮어 **전체-부분 관계**를 표현하는 패턴이다. </br></br>


## 언제 쓰이는가?
- 객체들 간에 계급 및 계층구조가 있고, 이를 표현해야 할 때
- 클라이언트가 단일 객체와 집합 객체를 구분하지 않고 동일한 형태로 사용하고자 할 때 </br>

> 대표적인 예시가 **디렉토리-파일 구조**
</br>


## 구조
- `Component` : Leaf 와 Composite가 구현해야하는 `Interface`로, Leaf와 Composite는 모두 Component라는 같은 타입으로 다뤄진다.
- `Leaf` : **단일 객체**로 Composite의 부분(자식) 객체로 들어가게 된다. (Component의 형태)
- `Composite` : **집합 객체**로 여러 Component 들을 가지기 때문에 Leaf 객체나 Composite 을 자식으로 둔다. 
  - 클라이언트는 Composite을 통해 부분 객체(Leaf, Composite)들을 다룬다.
![composite pattern](https://user-images.githubusercontent.com/102718303/210189346-cfa5d0c5-152a-44c1-8160-6af7c375479a.png)
![composite pattern2 png](https://user-images.githubusercontent.com/102718303/210189651-ab1c31d6-751c-4d89-b937-13796c8a94de.jpg)



### 예시
- 디렉토리-파일 구조를 예시로 들어보자.
- 구조의 Leaf 인 `File` 클래스 구현
- 구조의 Composite 인 `Directory` 클래스 구현
- 구조의 Component 인 `Node` 인터페이스 구현
```java
interface Node {
  public String getName();
}

/** 파일 클래스는 자식 요소를 가질 필요가 없기 때문에 인터페이스를 구현하면 끝 **/
class File implements Node {
  private String name;
  //...
  @Override
  public String getName() { return name; }
}

/** 디렉토리 클래스는 자식 요소를 담을 List 필요 **/
class Directory implements Node {
  private String name;
  private List<Node> children;
  //...
  @override
  public String getName() { return name; }
  public void add(Node node) {
    children.add(node);
  }
}

Directory dir = new Directory();
dir.add(new File());  // 디렉토리에 파일 삽입
dir.add(new Directory()); // 디렉토리에 디렉토리 삽입
Directory secondDir = new Direcory(); 
secondDir.add(dir); // 기존의 루트 디렉토리를 새로 만든 디렉토리에 삽입
```


## 장점
- 객체들이 모두 같은 타입으로 취급되기 때문에 새로운 클래스 추가가 쉽다.
- 단일 객체, 집합 객체 구분하지 않고 코드 작성이 가능하여 사용자 코드가 단순해진다.


## 단점
- 설계를 일반화 시켜 객체간의 구분, 제약이 힘들다.





## Reference
- https://dailyheumsi.tistory.com/193
- https://jdm.kr/blog/228
- https://mygumi.tistory.com/343


