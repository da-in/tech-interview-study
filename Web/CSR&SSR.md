# CSR & SSR

[렌더링(Rendering)](https://github.com/da-in/tech-interview-study/blob/main/Web/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%99%80%20%EB%A0%8C%EB%8D%94%EB%A7%81.md)은 브라우저가 서버에 요청한 페이지 자원을 화면에 표시하는 것을 말한다. `CSR`과 `SSR`은 렌더링의 한 방식이다. 웹 어플리케이션 유형은 페이지의 수에 따라 `SPA`와 `MPA`로 나뉘고, 이에 따라 렌더링 방식이 달라진다.

<br/>

## MPA(Multiple Page Application)

**MPA**는 여러 페이지로 구성된 전통적인 웹 어플리케이션을 말한다.  
사용자의 인터렉션을 통해 새로운 페이지를 요청하면 서버로부터 새로운 html을 받아와서 페이지 전체를 새로 렌더링한다.  
SSR(Server Side Rendering)방식으로 렌더링된다.

<br/>

## SPA(Single Page Application)

**SPA**는 하나의 페이지로 구성된 웹 어플리케이션을 말한다.  
최초에 한번 전체 페이지 리소스(HTML, CSS, JS...)를 로드하고, 이후부터는 **Ajax\*** 를 통해 비동기적으로 서버에서 필요한 데이터를 받은 후 **데이터 바인딩\***, 페이지 일부만을 동적으로 업데이트한다.
`React.js`, `Vue.js`, `Angular.js` 등의 프레임워크들이 SPA 방식을 사용한다.  
**CSR(Client Side Rendering)** 방식으로 렌더링된다.

> **Ajax**(Asynchronous JavaScript and XML)는 JavaScript와 XML을 이용해 비동기적으로 정보를 교환하는 방법, 기술을 의미한다. 오늘날 다양한 데이터 객체들도 사용 가능해지면서 XML보다 JSON 사용률이 더 커졌고, 약어와 기술간의 간극이 생기며 고유명사에 가깝게 사용되고 있다.
XMLHttpRequest API / jQuery / fetch API(ES2015 표준 등장) 등을 이용해 구현

> **Data Binding**은 두 데이터를 일치시키는 방법을 말하며, 단방향 데이터 바인딩과 양방향 데이터 바인딩이 있다.

<img src="https://user-images.githubusercontent.com/66757141/206862315-7dcfd719-bb5f-471e-8510-10378cc69f6c.png" alt="data binding" width="600px" />


<br/>

## SSR(Server Side Rendering)

**SSR**은 **Server Side Rendering**의 약자로, 렌더링이 서버 측면에서 이루어진다.  
페이지를 요청하면 서버는 페이지에 필요한 데이터를 가져와 모두 삽입하고, CSS까지 적용한 **렌더링 준비를 마친 HTML과 JS코드**를 클라이언트에게 전달한다.  
클라이언트는 전달받은 HTML 페이지를 출력하고 JS코드를 HTML에 실행한다.  
페이지 이동 및 변화시 페이지 전체를 **처음부터 다시 로드**한다.

<br/>

## CSR(Client Side Rendering)

**CSR**은 **Client Side Rendering**의 약자로, 렌더링이 클라이언트 측면에서 이루어진다.  
클라이언트는 서버로부터 페이지 요청 초기에 **모든 화면 표시에 필요한 모든 자원**을 받아와 렌더링한다.
페이지 이동 및 변화시, **Ajax를 통해 변화한 부분의 데이터만 받아오고 동일한 파일 상에서 DOM을 변경**하여 View를 업데이트한다.

<br/>

<img src="https://linked2ev.github.io/assets/img/devlog/201808/2018-08-01-SPA-step1.png" alt="SSR & CSR" width="450px" />

<br/>

## SSR과 CSR의 장단점

**SSR의 장점**

필요한 리소스만을 받아오므로 **초기 로딩 속도가 빠르다**.  
**검색엔진최적화(Search Engine Optimization, SEO)에 유리**하다. SEO를 위해 전체 페이지의 색인을 생성해야하는데, 이미 각각의 페이지가 분리되어 존재하기 때문이다.

**SSR의 단점**

페이지를 요청할 때마다 **새로고침** 되므로 깜빡임 등 **UX적으로 좋지 않다**.  
서버에서 페이지의 모든 리소스를 준비하여 응답하므로 **서버 부담이 증가**한다.  
SSR의 경우 완성된 형태의 웹을 받아와 바로 페이지를 출력하고 JS를 받아와 실행한다. 이때 **TTV(Time To View)와 TTI(Time To Interact) 간에 시간 간격**이 발생하게 된다. JS가 실행되기 전 까지 작동하지 않는 페이지가 사용자에게 보여지게 된다.

**CSR의 장점**

필요한 부분만을 주고 받기에 **서버의 부하가 비교적 적다**.  
초기화면 렌더링을 제외하면, **전반적인 렌더링 속도가 빠르다**.  
**TTV(Time To View)와 TTI(Time To Interact)가 일치한다**. CSR의 경우 빈 HTML 페이지를 받아온 후 JS에 의해 동적으로 페이지를 그리기 때문에, JS가 로드되어 사용가능한 시점에 사용자에게 보여진다.

**CSR의 단점**

모든 화면 출력에 필요한 자원을 받아오기에 **초기 화면 렌더링이 느리다**.  
JS 코드로 사용자와 상호작용을 해야 내용이 로드되므로, **SEO에 불리하다**.  
_(Google의 Search Engine 크롤러는 JS를 실행할 수 있어 SPA의 크롤링이 가능하다. 아직 일반적인 경우는 아니다.)_

<br/>

---

## Reference

📄https://miracleground.tistory.com/entry/SSR서버사이드-렌더링과-CSR클라이언트-사이드-렌더링  
📄https://hanamon.kr/spa-mpa-ssr-csr-장단점-뜻정리/  
📄https://hanamon.kr/네트워크-ajax란-spa를-만드는-기술/  
📄[Effects of Two-way Data Binding on Better User Experience and Easier Development of Clinical Information Systems | N. Omerbegovic, N. Omerbegovic, A. Subasi](https://www.semanticscholar.org/paper/Effects-of-Two-way-Data-Binding-on-Better-User-and-Omerbegovic-Omerbegovic/efb2e5476dfbc843950d9fa304b06e78cbfb75e7)
