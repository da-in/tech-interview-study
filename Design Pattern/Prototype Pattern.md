# 프로토타입 패턴(Prototype Pattern)

프로토타입 패턴은 객체의 생성 메커니즘을 다루는 **생성 패턴(Creational Pattern)** 이다.

**프로토타입** 은 '프로그램 등의 미완성 버전 또는 중요한 기능들이 포함되어 있는 초기모델'을 의미한다.

> 프로토타입 패턴(prototype pattern)은 소프트웨어 디자인 패턴 용어로, 생성할 객체들의 타입이 프로토타입인 인스턴스로부터 결정되도록 하며, 인스턴스는 새 객체를 만들기 위해 자신을 복제(clone)하게 된다. _wiki_

풀어서 말하면 다음과 같다.
프로토타입 패턴은 새로운 객체를 만들 때 비용이 많이 든다면, 처음부터 객체를 생성하는 것이 아니라 **원본 객체를 복사** 하여 수정하는 것이다.  
복사해서 사용할 수 있는 비슷한 객체가 존재할 때 해당 객체를 **프로토타입** 으로 사용하는 것이다.

<img src="https://user-images.githubusercontent.com/66757141/210564187-185a1622-6815-4b21-9709-1bf4c2eb091d.png" alt="1920px-Prototype_Pattern_ZP svg" />

<br/>

## 얕은 복사와 깊은 복사

디자인 패턴은 실질적인 구현 방법에 대한 명시가 아니기에, 프로토타입의 복사 방식은 개발자의 선택이다.  
Java에서는 일반적으로 clone() 메서드가 많이 사용된다.

<br/>

## 프로토타입 패턴을 사용하면 좋은 상황

1. 취급하는 오브젝트의 종류가 너무 많아, 각각을 별도의 클래스로 만들어 다수의 소스 파일을 작성해야 함
   클래스로부터 인스턴스 생성이 어려운 경우
2. 생성하고 싶은 인스턴스가 복잡한 작업을 거쳐 만들어지기 때문에, 클래스로부터 만들기가 매우 어려운 경우
   framework와 생성할 인스턴스를 분리하고 싶은 경우
3. 프레임워크를 특정 클래스에 의존하지 않고 만들고 싶은 경우. 클래스 이름을 지정하여 인스턴스를 만드는 것이 아니라, 이미 모형이 되는 인스턴스를 등록해 두고, 그 인스턴스를 복사하여 생성한다.

## 프로토타입 패턴 예시

```java
// Reference https://www.geeksforgeeks.org/prototype-design-pattern/
abstract class Color implements Cloneable {
    protected String colorName;
    abstract void addColor();
    public Object clone() { // clone
        Object clone = null;
        try {
            clone = super.clone();
        } catch (CloneNotSupportedException e) { // clone 불가시 예외 처리
            e.printStackTrace();
        }
        return clone;
    }
}

class blueColor extends Color {
    public blueColor() {
        this.colorName = "blue";
    }
    @Override
    void addColor() {
        System.out.println("Blue color added");
    }
}

class blackColor extends Color {
    public blackColor() {
        this.colorName = "black";
    }
    @Override
    void addColor() {
        System.out.println("Black color added");
    }
}

class ColorStore {
    private static Map<String, Color> colorMap = new HashMap<String, Color>();
    static {
        colorMap.put("blue", new blueColor());
        colorMap.put("black", new blackColor());
    }
    public static Color getColor(String colorName) {
        return (Color) colorMap.get(colorName).clone();
    }
}


// Driver class
class Prototype {
    public static void main (String[] args) {
        ColorStore.getColor("blue").addColor();
        ColorStore.getColor("black").addColor();
        ColorStore.getColor("black").addColor();
        ColorStore.getColor("blue").addColor();
    }
}
```

<br/>

---

## Reference

📄 https://yeah.tistory.com/17  
📄 https://ko.wikipedia.org/wiki/프로토타입  
📄 https://ko.wikipedia.org/wiki/프로토타입_패턴  
📄 https://velog.io/@newtownboy/디자인패턴-프로토타입패턴Prototype-Pattern  
📄 https://www.geeksforgeeks.org/prototype-design-pattern/
