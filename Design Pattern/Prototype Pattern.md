# 프로토타입 패턴(Prototype Pattern)

프로토타입 패턴은 객체의 생성 메커니즘을 다루는 **생성 패턴(Creational Pattern)** 이다.

**프로토타입** 은 '프로그램 등의 미완성 버전 또는 중요한 기능들이 포함되어 있는 초기모델'을 의미한다.

> 프로토타입 패턴(prototype pattern)은 소프트웨어 디자인 패턴 용어로, 생성할 객체들의 타입이 프로토타입인 인스턴스로부터 결정되도록 하며, 인스턴스는 새 객체를 만들기 위해 자신을 복제(clone)하게 된다. _wiki_

풀어서 말하면 다음과 같다.
프로토타입 패턴은 새로운 객체를 만들 때 비용이 많이 든다면, 처음부터 객체를 생성하는 것이 아니라 **원본 객체를 복사** 하여 수정하는 것이다.  
복사해서 사용할 수 있는 비슷한 객체가 존재할 때 해당 객체를 **프로토타입** 으로 사용하는 것이다.

## UML Diagram

<img src="https://user-images.githubusercontent.com/66757141/210564187-185a1622-6815-4b21-9709-1bf4c2eb091d.png" alt="1920px-Prototype_Pattern_ZP svg" width="600px"/>

<br/>
UML Diagram의 각 요소는 다음과 같다.

- **Prototype** - 복제하려는 인터페이스를 정의하며, clone 메서드를 선언하는 추상 클래스를 만든다.
- **Concrete Prototype** - 복제하는 연산을 구현한다.
- **Client** - 복제를 요청하여 새로운 객체를 생성한다.

<br/>

## 얕은 복사와 깊은 복사

디자인 패턴은 실질적인 구현 방법에 대한 명시가 아니기에, 프로토타입의 복사 방식은 개발자의 선택이다.

프로그래밍 언어에서 요소를 복사할 때에는 일반적으로 `깊은 복사`와 `얕은 복사`가 있다.

깊은 복사(Deep Copy)는 **실제 값** 을 새로운 메모리 공간에 복사하는 것을 의미하고, 얕은 복사(Shallow Copy)는 단순히 '주소값'을 복사하여 같은 값을 참조하는 방식이다. 얕은 복사를 할 경우 복사한 객체를 수정하면 원본 객체의 값도 함께 수정된다.

**Prototype Pattern을 구현할 때 원본 객체의 수정을 막으려면 깊은 복사를 사용해야한다.** Java의 경우 `clone()` 메서드를 활용한다. `clone()` 메서드 자체는 배열을 제외하고는 기본적으로 얕은 복사를 수행한다. 하지만 clonable 인터페이스\*를 implement하여 clone() 메서드를 오버라이딩 하면 깊은 복사를 사용할 수 있다.

\* _**clonable interface**는 상속받은 클래스가 복제해도 되는 클래스임을 명시하기위한 믹스인 인터페이스(다른 클래스에서 사용할 목적으로 만들어진 클래스)이다._

<br/>

## 프로토타입 패턴을 사용하면 좋은 상황

1. 취급하는 **오브젝트의 종류가 너무 많아** 각각을 별도의 클래스로 만들어 다수의 소스 파일을 작성해야 하는 경우
2. 클래스로부터 생성하고 싶은 **인스턴스가 복잡한 작업을 거쳐 만들기가 매우 어려운 경우**
3. 프레임워크를 특정 클래스에 의존하지 않고 만들고 싶은 경우. 클래스 이름을 지정하여 인스턴스를 만드는 것이 아니라, 이미 모형이 되는 인스턴스를 등록해 두고, 그 인스턴스를 복사하여 생성한다.

<br/>

## 프로토타입 패턴 예시

```java
/** Prototype Class **/
public class Cookie implements Cloneable {
   public Object clone() {
      try {
         Cookie copy = (Cookie)super.clone();
         return copy;
      }
      catch(CloneNotSupportedException e) {
         e.printStackTrace();
         return null;
      }
   }
}
```

```java
/** Concrete Prototypes to clone **/
public class CoconutCookie extends Cookie {
  ...
}
```

```java
/** Client Class**/
public class CookieMachine {
   private Cookie cookie; //could have been a private Cloneable cookie;
   public CookieMachine(Cookie cookie) {
      this.cookie = cookie;
   }
   public Cookie makeCookie() {
      return (Cookie)cookie.clone();
   }
   public Object clone() { }

   public static void main(String args[]) {
      Cookie tempCookie =  null;
      Cookie prot = new CoconutCookie();
      CookieMachine cm = new CookieMachine(prot);
      for (int i=0; i<100; i++)
         tempCookie = cm.makeCookie();
   }
}
```

<br/>

정리하면 다수의 객체를 `new` 키워드로 생성하는 것은 중복된 자원소모가 발생하여 비효율적이다. 이때 **프로토타입 패턴** 을 이용하여 객체를 `깊은 복사`하여 사용하면, 구현 클래스에 직접 연결하지 않고 객체를 복사할 수 있고, 중복되는 초기화 코드를 제거할 수 있다. 결과적으로는 복잡한 오브젝트를 보다 편리하게 만들수 있습니다. 단, 순환 참조가 있는 복잡한 객체를 복제하는 것은 까다로울 수 있다.

<br/>

---

## Reference

📄 https://yeah.tistory.com/17  
📄 https://ko.wikipedia.org/wiki/프로토타입  
📄 https://ko.wikipedia.org/wiki/프로토타입_패턴  
📄 https://velog.io/@newtownboy/디자인패턴-프로토타입패턴Prototype-Pattern  
📄 https://www.geeksforgeeks.org/prototype-design-pattern/  
📄 https://m.blog.naver.com/scw0531/221465259625
