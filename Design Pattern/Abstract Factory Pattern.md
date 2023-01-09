# Abstract Factory Pattern

**추상 팩토리 패턴** 은 생성 패턴으로, [팩토리 메소드 패턴](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/Factory%20Method%20Pattern.md)과 함께 [Simple Factory](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/Factory%20Method%20Pattern.md)와 관련있는 패턴이다.

**팩토리 메소드 패턴** 은 어떠한 객체를 생성할 것인지를 하위 클래스에 위임하는데에 핵심이 있었다. 결론적으로 서로 다른 클래스의 동일한 메소드로 서로 다른 객체를 생성할 수 있었다.

**추상 팩토리 패턴** 은 이와 유사하지만, 연관 관계를 가진 **객체의 집합** 을 생성하는데에 중점을 둔다.

<br/>

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

<br/>

---

## Reference

📄https://bcp0109.tistory.com/368  
📄https://kotlinworld.com/366  
📄https://whereami80.tistory.com/211  
📄https://stackoverflow.com/questions/5739611/what-are-the-differences-between-abstract-factory-and-factory-design-patterns
