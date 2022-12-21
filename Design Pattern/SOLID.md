# 객체지향 5원칙(SOLID)
객체지향에서 꼭 지켜야 할 5개의 원칙을 통틀어 객체지향 5원칙이라 칭하며, 앞글자를 따서 SOLID라고도 부른다. <br/>
이 원칙들을 철저히 지키면 시간이 지나도 변경이 용이하고, 유지보수와 확장이 쉬운 소프트웨어를 개발하는데 도움이 된다.

## 단일 책임 원칙 (Single Responsibility Principle) : SRP
**객체는 오직 하나의 책임을 가져야 한다.<br/>즉, 객체는 오직 하나의 변경의 이유만을 가져야한다.**
- 하나의 책임? : 변경을 기준으로! => 어떠한 역할에 대해 변경사항이 발생했을 때, 영향을 받는 기능만 모아두자.
- 다른 클래스들이 서로 영향을 미치는 연쇄 작용을 줄일 수 있다.
- 응집도는 높이고 결합도는 낮출 수 있다!

as-is<br/>
![화면 캡처 2022-12-20 172451](https://user-images.githubusercontent.com/50827930/208619660-2b6ea431-db0e-45d2-9415-9714b07e2820.png)

to-be<br/>
![화면 캡처 2022-12-20 172523](https://user-images.githubusercontent.com/50827930/208619669-44cdafcc-065d-4f21-b5d1-cae63a6b52a8.png)

## 개방 폐쇄 원칙 (Open/Closed Principle) : OCP
**객체는 확장에 대해서는 개방적이고 수정에 대해서는 폐쇄적이어야 한다. (객체 기능의 확장은 허용하고 스스로의 변경은 피한다)**
- 확장에 대해서 개방적이다 : 요구사항이 변경될 때 새로운 동작을 추가하여 애플리케이션의 기능을 확장할 수 있다.
- 수정에 대해서 폐쇄적이다 : 기존의 코드를 수정하지 않고 애플리케이션의 동작을 추가하거나 변경할 수 있다.
- 개방 폐쇄 원칙을 지키기 위해서는 추상화에 의존해야한다!<br/>
  (※추상화 : 핵심적인 부분만 남기고 불필요한 부분은 제거하여 복잡한 것을 간단히 하는 것)<br/>
  추상화를 통해 변하는 것들은 숨기고, 변하지 않는 것들에 의존하게 하자.<br/>
  => 우리는 기존의 코드 및 클래스들을 수정하지 않은 채로 애플리케이션을 확장할 수 있다.

as-is<br/>
![image](https://user-images.githubusercontent.com/50827930/208619790-a5330087-dc06-4890-a2c0-167db31d2f61.png)

to-be<br/>
![image](https://user-images.githubusercontent.com/50827930/208619849-e388a4af-84d3-448e-a1d9-b7332fe045d8.png)


## 리스코프 치환 원칙 (Liskov Substitution Principle) : LSP
**자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있다. <br/> 이 말은, 부모 클래스가 들어갈 자리에 자식 클래스를 넣어도 계획대로 잘 작동한다**
- 즉, 부모 클래스를 상속한 자식 클래스는 부모 클래스의 역할을 정확히 해내야한다.

as-is<br/>
![image](https://user-images.githubusercontent.com/50827930/208620145-44977f0c-d488-4b15-945d-fd94d3be83cf.png)

to-be<br/>
![image](https://user-images.githubusercontent.com/50827930/208620266-b8145e77-a719-40c5-bb86-fb7a11fa43fa.png)

## 인터페이스 분리 원칙 (Interface Segregation Principle) : ISP
**객체가 충분히 높은 응집도의 작은 단위로 설계됐더라도, 목적과 관심이 각기 다른 클라이언트가 있다면 인터페이스를 통해 적절하게 분리해줄 필요가 있다.**
- 자신이 사용하지 않는 인터페이스는 구현하지 말아야한다.
- 하나의 큰 인터페이스를 상속 받기 보다는 인터페이스를 구체적이고 작은 단위들로 분리시켜 꼭 필요한 인터페이스만 상속하자.

![image](https://user-images.githubusercontent.com/50827930/208620350-8acebf57-88b8-4c7c-b91b-d7693864dcb3.png)

## 의존관계 역전 원칙 (Dependency Inversion Principle) : DIP
**고수준 모듈은 저수준 모듈에 의존해선 안되며, 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야 한다.**
- 고수준 모듈 : 변경이 없는 추상화된 클래스(또는 인터페이스)
- 저수준 모듈 : 변하기 쉬운 구체 클래스
- 즉, 의존 역전 원칙이란 결국 추상화에 의존하며 구체화에는 의존하지 않는 설계 원칙을 의미한다.

as-is<br/>
![image](https://user-images.githubusercontent.com/50827930/208620502-b5c9a5d9-490f-45c5-9645-d51a1b068782.png)

to-be<br/>
![image](https://user-images.githubusercontent.com/50827930/208620606-93879357-91ca-430d-a135-b63a03469758.png)


## Reference
- https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9B%90%EC%B9%99
- https://mangkyu.tistory.com/194
- https://jaeyeong951.medium.com/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-5%EC%9B%90%EC%B9%99-solid-ac7d4d660f4d
- https://youngjinmo.github.io/2021/04/principles-of-oop/
- https://devlog-wjdrbs96.tistory.com/380
