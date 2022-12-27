# 싱글톤 패턴 (Singleton pattern)

- 애플리케이션이 시작될 때
    1. 어떤 클래스가 최초 한 번만 메모리를 할당하고
    2. 해당 메모리에 인스턴스를 만들어 사용하는 패턴
- 즉, ‘하나’의 클래스가 ‘하나’의 인스턴스만 생성하여 사용하는 디자인 패턴
- 인스턴스가 필요할 때, 똑같은 인스턴스를 만들지 않고 기존의 인스턴스를 활용하게 된다.
- 생성자가 여러번 호출되도, 실제로 생성되는 객체는 하나!
    
    최초로 생성된 이후에 호출된 생성자는 이미 생성한 객체를 반환시키도록 만드는 것이다.
    

## 특징

- 객체 자체에는 접근이 불가능해야 함.(Private)
- 객체에 대한 접근자를 사용해 실제 객체를 제어할 수 있다.
- 객체는 단 하나만 만들어지며, 해당 객체를 공유함
- 싱글톤으로 구현한 인스턴스는 ‘전역(global)’이다.
    
    따라서, 다른 클래스의 인스턴스들이 데이터를 공유하는 것이 가능하다.
    

## 근데.. 이걸 왜 써?

- 보통의 경우, 객체를 생성할 때마다 메모리 영역을 할당 받는다.
- 싱글톤 패턴의 경우 한번의 객체 생성을 하고, 그 객체를 공유한다.
- 따라서 메모리 낭비를 방지할 수 있다. (+ 속도도 빨라)
- 그렇기 때문에, 주로 공통된 객체를 여러개 생성해서 사용해야하는 상황에 많이 사용
    
    (쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체등)
    
- 아니면 인스턴스가 절대적으로 한 개만 존재하는 것을 보증하고 싶을 때

## 단점..

- 객체지향 5원칙(SOLID)에서 보면 개방-폐쇄 원칙이란 것이 존재한다.
- 싱글톤 인스턴스가 혼자 너무 많은 일을 하거나, 많은 데이터를 공유시키면 다른 클래스들 간의 결합도가 높아진다.
    
    → 이는 개방-폐쇄 원칙을 위반하는 것이다. (객체 지향적으로 설계하지 않았다는 것)
    
    → 따라서 수정이 어려워지고 테스트하기 어려워진다.
    
- 또한, 멀티 스레드 환경에서 동기화 처리를 하지 않았을 때, 인스턴스가 2개가 생성되는 문제도 발생할 수 있다. (동시성 문제)
- 따라서, 반드시 싱글톤이 필요한 상황이 아니면 지양하는 것이 좋다고 한다. 
  
  (설계 자체에서 싱글톤  활용을 원활하게 할 자신이 있으면 괜찮고)

## 자바스크립트에서의 싱글톤..

```jsx
const SingletonClass = (function() {
  let instance;

  function init(){ // 싱글톤 객체를 리턴할 비공개 함수
    return {
      publictMethod: function() {
        return 'public method';
      },
      publicProp: 'public variable',
    };
  }

  return {
    getInstance: function() { //클로저
      if (instance) {
        return instance; // 있으면 그냥 반환
      }
      instance = init();
      return instance; // 없으면 객체 생성 후 반환 (이해를 위해 명시적으로 나눔)
    }
  };
})(); //즉시 실행 함수

const a = SingletonClass.getInstance();
console.log(a.publicProp, 'a'); // 'public variable'

const b = SingletonClass.getInstance();
console.log(a === b) // true
```

## Reference

- [https://gyoogle.dev/blog/design-pattern/Singleton Pattern.html](https://gyoogle.dev/blog/design-pattern/Singleton%20Pattern.html)
- [https://inpa.tistory.com/entry/OOP-💠-아주-쉽게-이해하는-OCP-개방-폐쇄-원칙](https://inpa.tistory.com/entry/OOP-%F0%9F%92%A0-%EC%95%84%EC%A3%BC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EB%8A%94-OCP-%EA%B0%9C%EB%B0%A9-%ED%8F%90%EC%87%84-%EC%9B%90%EC%B9%99)
- [https://velog.io/@seongwon97/싱글톤Singleton-패턴이란](https://velog.io/@seongwon97/%EC%8B%B1%EA%B8%80%ED%86%A4Singleton-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80)
- [https://velog.io/@ggong/자바스크립트에서-싱글톤-패턴-이해하기](https://velog.io/@ggong/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-%EC%8B%B1%EA%B8%80%ED%86%A4-%ED%8C%A8%ED%84%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
- [https://heecheolman.tistory.com/40](https://heecheolman.tistory.com/40)
