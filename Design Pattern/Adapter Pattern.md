# 어댑터 패턴(Adapter Pattern)

> *GoF 책에서는 다음과 같이 패턴을 설명한다.*   
클래스의 인터페이스를 사용자가 기대하는 인터페이스 형태로 **적응(변환)** 시킵니다.   
서로 일치하지 않는 인터페이스를 갖는 클래스들을 함께 동작시킵니다.

>*헤드 퍼스트 디자인 패턴에서는 다음과 같이 정의한다*  
한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 **변환** 합니다.  
어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있습니다.

## 요약
특정 인터페이스를 지원하지 않는 대상 객체를 인터페이스를 지원하는 Adapter에 집어넣어서 사용하는 방법이라 할 수 있다.

다음은 헤드 퍼스트 디자인 패턴에서의 예시 다이어그램이다.  
<img width="548" alt="스크린샷 2023-01-02 오후 4 44 02" src="https://user-images.githubusercontent.com/70997596/210206077-92761944-bced-41b3-be63-a1f0d9c354d9.png">

- Client는 Target 인터페이스를 구현한 Adaptee가 필요하다.
- Adaptee는 Target인터페이스를 구현하지 않고 있다.
    - Adaptee는 이미 개발이 완료되어 사용중이다.
    - Adaptee를 변경하는 것이 적절하지 않은 상황이다.

예시 코드)

다음은 오리를 표현한 인터페이스다.
```java
interface Duck {
  public void quack();  // 오리는 꽉꽉 소리를 낸다
  public void fly();
}

class MallardDuck implements Duck {
  @Override
  public void quack() {
    System.out.println("Quack");
  }
  @Override
  public void fly() {
    System.out.println("I'm flying");
  }
}
```

다음은 칠면조를 표현한 인터페이스다.
```java
interface Turkey {
  public void gobble();   // 칠면조는 골골거리는 소리를 낸다
  public void fly();
}

class WildTurkey implements Turkey {
  @Override
  public void gobble() {
    System.out.println("Gobble gobble");
  }
  @Override
  public void fly() {
    System.out.println("I'm flying a short distance");
  }
}
```

마지막으로, 어댑터를 살펴보자
```java
class TurkeyAdapter implements Duck {
  Turkey turkey;

  public TurkeyAdapter(Turkey turkey) {
    this.turkey = turkey;
  }
  @Override
  public void quack() {
    turkey.gobble();
  }
  @Override
  public void fly() {
    // 칠면조는 멀리 날지 못하므로 다섯 번 날아서 오리처럼 긴 거리를 날게 한다
    for (int i = 0; i < 5; i++) {
      turkey.fly();
    }
  }
}
```
<img width="531" alt="스크린샷 2023-01-02 오후 4 50 39" src="https://user-images.githubusercontent.com/70997596/210206096-06bac66e-5a77-49b8-98c8-08f2a6f7322e.png">



사용예시
- Enumeration
- 상속을 사용하는 기법

##출처
https://johngrib.github.io/wiki/pattern/adapter/#fn:joshua-334
