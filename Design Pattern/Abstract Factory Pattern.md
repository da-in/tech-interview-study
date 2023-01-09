# (추상 팩토리 패턴)Abstract Factory Pattern

**추상 팩토리 패턴** 은 생성 패턴으로, [팩토리 메소드 패턴](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/Factory%20Method%20Pattern.md)과 함께 [Simple Factory](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/Factory%20Method%20Pattern.md)와 관련있는 패턴이다.

<br/>

## 차이

**팩토리 메소드 패턴** 은 어떠한 객체를 생성할 것인지를 하위 클래스에 위임하는데에 핵심이 있었다. 결론적으로 팩토리 메소드 패턴은 서로 다른 객체를 생성할 수 있는 **`메소드`** 를 제공한다. 그리고 메소드를 통해 하나의 객체를 생성한다.

**추상 팩토리 패턴** 은 이와 유사하지만, 연관 관계를 가진 **`객체의 집합`** 을 생성하는데에 중점을 둔다. 구현하고자 하는 객체의 하위클래스(Factory)를 생성하고, 원하는 하위 클래스를 결합하는 형태이다. 그래서 팩토리 클래스는 여러개의 팩토리 메소드를 갖는 형태가 된다.

<br/>

![abstract](https://user-images.githubusercontent.com/66757141/211338561-e3b4a4c8-5126-4561-bc88-ff4d1962afa0.png)<br/>
_[Reference](https://www.dofactory.com/net/abstract-factory-design-pattern)_

```java
public interface Monitor { }
public class NormalMonitor implements Monitor { }
public class GamingMonitor implements Monitor { }

public interface Mouse { }
public class NormalMouse implements Mouse { }
public class GamingMouse implements Mouse { }
```

```java
public interface ComputerFactory {
    Monitor createMonitor();
    Mouse createMouse();
}

public class NormalComputerFactory extends ComputerFactory {
    @Override
    public Monitor createMonitor(){
      return new NormalMonitor();
    }
    @Override
    public Mouse createMouse(){
      return new NormalMouse();
    }
}

public class GamingComputerFactory extends ComputerFactory {
    @Override
    public Monitor createMonitor(){
      return new GamingMonitor();
    }
    @Override
    public Mouse createMouse(){
      return new GamingMouse();
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        ComputerFactory normalComputerFactory = new NormalComputerFactory();
        ComputerFactory gamingComputerFactory = new GamingComputerFactory();

        Monitor normalMonitor = normalComputerFactory.createMonitor();
        Mouse normalMouse = normalComputerFactory.createMouse();

        Monitor gamingMonitor = gamingComputerFactory.createMonitor();
        Mouse gamingMouse = gamingComputerFactory.createMouse();
    }
}
```

<br/>

## 추상 팩토리 패턴 장단점

**추상 팩토리 패턴** 도 팩토리 메서드 패턴과 마찬가지로 기존 코드를 수정하지 않고 확장할 수 있어 개방 폐쇄 원칙(Open-Closed Principle, OCP)을 지킨다. 또한 여러 개의 비슷한 **집합 객체** 생성을 하나의 팩토리에 모아둘 수 있다.

팩토리 메서드 패턴과 동일하게 구현하는 클래스의 개수, **코드량이 증가** 한다는 단점이 있다. Factory 클래스가 한 종류만 필요할 경우에는 비효율적인 방식이다.

**팩토리 메서드 패턴** 과 **추상 팩토리 패턴** 은 무엇이 더 좋다고 구분할 수 없고, 주어진 상황에 적합한 패턴을 선택하여 사용해야한다.

<br/>

---

## Reference

📄https://stackoverflow.com/questions/5739611/what-are-the-differences-between-abstract-factory-and-factory-design-patterns  
📄https://bcp0109.tistory.com/368  
📄https://kotlinworld.com/366  
📄https://whereami80.tistory.com/211  
📄https://www.dofactory.com/net/abstract-factory-design-pattern  
📄https://yeah.tistory.com/13
