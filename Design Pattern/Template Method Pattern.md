# 템플릿 메소드 패턴

> *GoF 책에서는 다음과 같이 패턴을 설명한다.*   
알고리즘의 구조를 메소드에 정의하고, 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 재정의 하는 패턴이다.  
알고리즘이 단계별로 나누어 지거나, 같은 역할을 하는 메소드이지만 여러곳에서 다른형태로 사용이 필요한 경우 유용한 패턴이다.

>*토비의 스프링에서는 다음과 같이 정의한다*  
상속을 통해 슈퍼클래스의 기능을 확장할 때 사용하는 가장 대표적인 방법.  
변하지 않는 기능은 슈퍼클래스에 만들어두고 자주 변경되며 확장할 기능은 서브클래스에서 만들도록 한다.

[사진]

템플릿 메소드의 전체적인 구조는 위와 같다.  
AbstractClass는 템플릿 메소드를 정의하며, 하위 클래스에서 알맞게 확장할 수 있는 메소드인 훅 메소드를 제공한다.  
여기서, 템플릿 메소드는 일반적인 메소드와 훅 메소드를 이용한다.   
그리고 ConcreteClass는 물려받은 훅 메소드를 재정의하는 역할을 한다.


```java
abstract class Teacher{
	
    public void start_class() {
        inside();
        attendance();
        teach();
        outside();
    }
	
    // 공통 메서드
    public void inside() {
        System.out.println("선생님이 강의실로 들어옵니다.");
    }
    
    public void attendance() {
        System.out.println("선생님이 출석을 부릅니다.");
    }
    
    public void outside() {
        System.out.println("선생님이 강의실을 나갑니다.");
    }
    
    // 추상 메서드
    abstract void teach();
}
 
// 국어 선생님
class Korean_Teacher extends Teacher{
    
    @Override
    public void teach() {
        System.out.println("선생님이 국어를 수업합니다.");
    }
}
 
//수학 선생님
class Math_Teacher extends Teacher{

    @Override
    public void teach() {
        System.out.println("선생님이 수학을 수업합니다.");
    }
}

//영어 선생님
class English_Teacher extends Teacher{

    @Override
    public void teach() {
        System.out.println("선생님이 영어를 수업합니다.");
    }
}

public class Main {
    public static void main(String[] args) {
        Korean_Teacher kr = new Korean_Teacher(); //국어
        Math_Teacher mt = new Math_Teacher(); //수학
        English_Teacher en = new English_Teacher(); //영어
        
        kr.start_class();
        System.out.println("----------------------------");
        mt.start_class();
        System.out.println("----------------------------");
        en.start_class();
    }
}
```

### 장점
1. 중복코드를 줄일 수 있다.

2. 자식 클래스의 역할을 줄여 핵심 로직의 관리가 용이하다.

3. 좀더 코드를 객체지향적으로 구성할 수 있다.

### 단점
1. 추상 메소드가 많아지면서 클래스 관리가 복잡해진다.

2. 클래스간의 관계와 코드가 꼬여버릴 염려가 있다.