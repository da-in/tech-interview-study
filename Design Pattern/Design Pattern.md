# Design Pattern

**소프트웨어 디자인 패턴(software design pattern)** 은 소프트웨어 공학의 소프트웨어 디자인에서 특정 문맥에서 공통적으로 발생하는 문제에 대한 **재사용 가능한 해결책** 이다.

> “바퀴를 다시 발명하지 마라(Don’t reinvent the wheel)”
> 이 관용적 어구는 이미 발명되었고 운영적 결함이 있다고 간주되지 않는 것의 재발명 시도는 불필요하다는 의미이다. 이전에 다른 사람들에 의해 만들어졌거나 최적화된 기초적인 방식을 복제하라는 것이다.

디자인 패턴은 프로그래머가 어플리케이션이나 시스템을 디자인할 때 사용하며, 실제적으로 구현된 내용이 아니라 문제 해결을 위한 형식화된 **관행** 이자 **템플릿** 이다. 기존에 잘 정리된 디자인 패턴을 사용하여 코드의 **재사용성** , **호환성** , **유지 보수성** 을 보장할 수 있다.

디자인 패턴은 [SOLID](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/SOLID.md) 원칙에 기반한다.

<br/>

## History

건축적 개념으로서의 패턴에서 시작하여 1987년부터 실험되고 정리되어왔으며, 1994년 GoF\*의 [Design Patterns: Elements of Reusable Object-Oriented Software](<https://ko.wikipedia.org/wiki/%EB%94%94%EC%9E%90%EC%9D%B8_%ED%8C%A8%ED%84%B4_(%EC%B1%85)>) 이 출판되고 인기를 끌었다.

_\* Design Patterns 책의 저자 Erich Gamma, Richard Helm, Ralph Johnson, John Vlissdes가 GoF(Gang of Four, 사인방)로 불린다._

<br/>

디자인 패턴은 콘텍스트, 문제, 해결을 기술한다.

- **콘텍스트(context)**  
  문제가 발생하는 상황을 기술한다. 즉, 패턴이 적용될 수 있는 상황, 유용하지 않은 상황 등을 나타낸다.

- **문제(problem)**  
  패턴으로 해결하고자 하는 여러 디자인 이슈들을 기술한다.

- **해결(solution)**
  문제를 해결하기 위한 설계(요소, 요소간의 관계, 책임, 협력 관계 등)를 기술한다. 이 때 해결은 구체적인 구현 방법이나 언어에 의존적이지 않으며 다양한 상황에 적용할 수 있는 일종의 템플릿이다.

<br/>

GoF의 Design Patterns에서는 객체지향적 디자인 패턴을 `생성 패턴(Creational Pattern)`, `구조 패턴(Structural Pattern)`, `행동 패턴(Behavioral Pattern)` 3가지로 구분한다.

|                                             생성 패턴                                              | 구조 패턴 |        행동 패턴        |
| :------------------------------------------------------------------------------------------------: | :-------: | :---------------------: |
| [Singleton](https://github.com/da-in/tech-interview-study/blob/main/Design%20Pattern/SingleTon.md) |  Adapter  | Chain-of-responsibility |
|                                          Abstract Factory                                          |  Bridge   |         Command         |
|                                           Factory Method                                           | Composite |       Interpreter       |
|                                              Builder                                               | Decorator |        Iterator         |
|                                             Prototype                                              |  Facade   |        Mediator         |
|                                                                                                    | Flyweight |         Memento         |
|                                                                                                    |   Proxy   |        Observer         |
|                                                                                                    |           |          State          |
|                                                                                                    |           |        Strategy         |
|                                                                                                    |           |     Template Method     |
|                                                                                                    |           |         Visitor         |

<br/>

## 생성 패턴(Creational Pattern)

생성 패턴은 객체의 생성 메커니즘을 다룬다. 객체의 생성 및 조합이 프로그램에 영향을 끼치지 않도록 분리하여 유연성을 높이고 코드의 유지/보수를 쉽게하기 위한 디자인 패턴이다.

<br/>

## 구조 패턴(Structural Pattern)

구조 패턴은 클래스나 객체등의 요소들의 관계를 용이하게 구조화하기 위한 디자인 패턴이다. 요소들을 조합하여 더 큰 구조를 만들 수 있게 한다.

<br/>

## 행동 패턴(Behavioral Pattern)

행위 패턴은 클래스나 객체들의 상호작용을 위한 알고리즘, 책임 분배 등을 정의하는 패턴이다

<br/>

---

## Reference

📄https://readystory.tistory.com/114  
📄https://velog.io/@wooko5/GoF-Design-Pattern-%EC%9D%B4%EB%9E%80  
📄https://ko.wikipedia.org/wiki/소프트웨어_디자인_패턴  
📄https://gmlwjd9405.github.io/2018/07/06/design-pattern.html
