# 팩토리 메소드 패턴(Factory Method Pattern)

디자인 패턴에서 팩토리와 관련된 패턴은 `팩토리 메소드 패턴(Factory Method Pattern)`과 `추상 팩토리 패턴(Abstract Factory Pattern)` 두 가지가 있다.
이 두 가지 패턴의 기본이 되는 `Simple Factory`가 있다. 객체지향 프로그래밍을 할 때에 관용구 처럼 사용되는 개념으로 디자인 패턴으로 취급되지는 않는다.
그래서 `Simple Factory`를 이해한 후 팩토리 메소드 패턴과 [추상 팩토리 패턴](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/Abstract%20Factory%20Pattern.md)을 알아본다.

<br/>

## Simple Factory

객체를 생성할 때 직접 생성자를 호출하면, 생성 로직에 변화가 생겼을 때 객체를 생성한 모든 부분의 코드를 수정해야한다.  
그래서 생성자 호출을 담당하는 `Factory` 클래스를 둔 후 이를 통해서 객체를 생성하는 방식이다.

<img src="https://user-images.githubusercontent.com/66757141/211150071-0ffa299b-bf7a-4ec8-ade4-ea0bdf34a7e8.png" alt="simplefactorystructure11_waifu2x_art_noise2_scale" width="700px" /><br/>
[_UML Reference_](https://sites.google.com/site/haithamraik/Home/design-pattern-list/simple-factory)

<br/>

```java
public interface Laptop {
    void runTests();
}

public class NormalLaptop implements Laptop {
    @Override
    public void runTests() {
       System.out.println("Running tests on a NormalLaptop...");
    }
}

public class GamingLaptop implements Laptop {
    @Override
    public void runTests() {
       System.out.println("Running tests on a GamingLaptop...");
    }
}
```

```java
public class LaptopFactory {
    // Objects are created here
    public Laptop createLaptop(String laptopType){
        if (laptopType == null) {
            return null;
        }
        switch (laptopType.toUpperCase()) {
            case "NormalLaptop":
                return new NormalLaptop();
                break;
            case "GamingLaptop":
                return new GamingLaptop();
                break;
            default:
                return null;
        }
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        LaptopFactory laptopFactory = new LaptopFactory();
        // Get object of type GamingLaptop and run tests.
        Laptop myLaptop = laptopFactory.createLaptop("GamingLaptop");
        myLaptop.runTests();
    }
}
```

`Simple Factory`를 사용하면 `Client`가 구현 클래스에 직접 의존하지 않기 때문에 생성자에 변화가 생겨도 `Factory` 클래스만 수정하면 된다.

`Simple Factory`는 [객체 지향 5원칙 SOLID](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/SOLID.md)의 개방 폐쇄 원칙(Open-Closed Principle, OCP)에 위배된다. 구현 클래스가 추가 및 수정되었을 때 Factory 클래스를 수정해주어야하기 때문이다.

이 때 `팩토리 메소드 패턴`이나 `추상 팩토리 패턴`을 사용하면 기존 클래스를 수정하지 않고 확장할 수 있다.

<br/>

## Factory Method Pattern

**팩토리 메소드 패턴** 은 생성 패턴 중 하나로, 객체를 생성할 때 어떤 클래스의 인스턴스를 만들 지 서브 클래스에서 결정하도록 한다. 즉 인스턴스의 생성을 서브클래스에게 위임한다.

<img src="https://user-images.githubusercontent.com/66757141/211150215-5fbda378-c195-4da4-b002-542b4a75490e.png" alt="N3mC1_waifu2x_art_noise2_scale" width="700px" /><br/>
[_UML Reference_](https://www.dofactory.com/net/factory-method-design-pattern)

앞선 `Simple Factory` 예제의 `Laptop` 인터페이스와 `NormalLaptop`, `GamingLaptop` 클래스가 있다고 했을 때 팩토리 메소드 패턴을 적용하면 아래와 같다.

```java
public abstract class LaptopFactory {
    public Laptop newInstance(){
        Laptop laptop = createLaptop();
        laptop.runTests();
        return laptop;
    }
    protected abstract Laptop createLaptop();
}

public class NormalLaptopFactory extends LaptopFactory {
    @Override
    protected User createLaptop() {
        return new NormalLaptop();
    }
}

public class GamingLaptopFactory extends LaptopFactory {
    @Override
    protected User createLaptop() {
        return new GamingLaptop();
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        LaptopFactory normalLaptopFactory = new NormalLaptopFactory();
        Laptop normalLaptop = normalLaptopFactory.newInstance();

        LaptopFactory gamingLaptopFactory = new GamingLaptopFactory();
        Laptop gamingLaptop = gamingLaptopFactory.newInstance();
        myLaptop.runTests();
    }
}
```

팩토리 메소드 패턴의 장점은 기존의 코드를 수정하지 않고 확장이 가능하여 개방 폐쇄 원칙(Open-Closed Principle, OCP)을 위반하지 않는다는 것이다. 결과적으로 팩토리 클래스를 통해 하나의 메소드(`ex. newInstance()`)를 사용해서 여러 종류의 객체를 생성할 수 있다.

단 패턴을 구현하기 위해 더 많은 클래스를 정의해야 하기 때문에 코드량이 증가하고 복잡해진다는 단점이 있다.

<br/>

---

## Reference

📄https://bcp0109.tistory.com/366  
📄https://bcp0109.tistory.com/367  
📄https://sites.google.com/site/haithamraik/Home/ design-pattern-list/simple-factory  
📄https://dragonprogrammer.com/design-patterns-java-simple-factory/  
📄https://www.dofactory.com/net/factory-method-design-pattern
