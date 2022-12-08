# Cross Browsing

## Cross Browsing

크로스 브라우징은 HTML, CSS, Javascript 작성 시 W3C의 웹 표준 규격에 맞도록 작성하며, 제작한 웹페이지가 서로 다른 환경을 가진 브라우저들에서 의도한 대로 작동하도록 하는 작업을 말한다.

브라우저 마다 [랜더링 엔진](https://github.com/da-in/tech-interview-study/blob/main/Web/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%99%80%20%EB%A0%8C%EB%8D%94%EB%A7%81.md)이 다르기 때문에, 작동되지 않는 HTML5, JS 코드와 해석하지 못하는 CSS 코드가 존재할 수 있다. 브라우저에 따른 버그가 존재할 수 있고, 브라우저 자체 CSS 차이의 영향을 받을 수 있다.

국내 블로그 자료들에서는 **크로스-브라우징**(Cross Browsing)이라는 표현을 많이 사용하였으나, 해외에서는 아래의 **크로스-브라우저 테스팅**(Cross-browser Testing), **크로스-브라우저 호환성**(Cross-browser Compatibility)의 표현을 주로 사용하였다.

#### Cross-browser Compatibility

Cross Browsing을 통해 보장하고자 하는 브라우저 간의 호환성을 의미한다.

#### Cross-browser Testing

Cross-browser Compatibility를 보장하기 위해 진행하는 테스팅 기법을 뜻한다.  
주로 QA 엔지니어에 의해 수행된다.

<br/>

## 크로스 브라우징에 대한 오해

크로스브라우징은 완전한 동일성을 의미하는 것이 아니라 최소한 핵심 기능의 사용은 보장하는 동등성을 의미한다. 페이지가 완전히 똑같이 보이게 하는 것이 아님에 유의해야한다.  
예를 들어 동일한 페이지가 특정 브라우저에서 더 좋아 보일 수 있다. 하지만 정도의 차이가 있더라도 모든 브라우저에서 읽는 행위는 가능해야한다.

> ex - Modern Browser에서의 입체 애니메이션과, 구형 브라우저에서의 평면 그래픽.

<br/>

## 렌더링 엔진(레이아웃 엔진)

서로 다른 브라우저여도 동일한 렌더링 엔진을 사용한다면 비슷한 결과를 얻을 수 있다.

![화면 캡처 2022-12-09 041556](https://user-images.githubusercontent.com/66757141/206547114-5d26cf01-dfc0-4867-8641-3547e9e38570.png)
_Comparison of browser engines [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_browser_engines)_

**Active Status**는 새로운 웹 표준이 엔진에 추가되어 멀티미디어를 포함한 대다수의 웹사이트를 렌더링할 수 있음을 의미한다.  
**Maintained Status**는 적어도 엔진이 여전히 컴파일 됨을 의미한다.  
**Discontinued**는 엔진의 제공이 중단되었음을 의미한다.

<br/>

---

## Reference

📄 https://blog.naver.com/insaweb/221926915225  
📄 https://github.com/Songwonseok/CS-Study/blob/main/Web/%ED%81%AC%EB%A1%9C%EC%8A%A4%20%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A7%95.md
📄 https://mulder21c.github.io/2019/01/30/what-is-cross-browsing/
