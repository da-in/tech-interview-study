# Cross Browsing

## Cross Browsing

크로스 브라우징은 HTML, CSS, Javascript 작성 시 W3C의 웹 표준 규격에 맞도록 작성하며, 제작한 웹페이지가 서로 다른 환경을 가진 브라우저들에서 의도한 대로 작동하도록 하는 작업을 말한다.

브라우저 마다 [랜더링 엔진](https://github.com/da-in/tech-interview-study/blob/main/Web/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%99%80%20%EB%A0%8C%EB%8D%94%EB%A7%81.md)이 다르기 때문에, 작동되지 않는 HTML5, JS 코드와 해석하지 못하는 CSS 코드가 존재할 수 있다. 브라우저에 따른 버그가 존재할 수 있고, 브라우저 자체 CSS 차이의 영향을 받을 수 있다.

국내 블로그 자료들에서는 **크로스-브라우징**(Cross Browsing)이라는 표현을 많이 사용하였으나, 해외에서는 아래의 **크로스-브라우저 테스팅**(Cross-browser Testing), **크로스-브라우저 호환성**(Cross-browser Compatibility)의 표현을 주로 사용하였다.

**Cross-browser Compatibility**  
Cross Browsing을 통해 보장하고자 하는 브라우저 간의 호환성을 의미한다.

**Cross-browser Testing**  
Cross-browser Compatibility를 보장하기 위해 진행하는 **테스팅 기법**을 뜻하며 일반적으로 **QA 엔지니어**에 의해 수행된다.  
글꼴 및 이미지의 표시, 반응형 웹 디자인 작동 여부 등 **콘텐츠 및 레이아웃의 일관성**을 테스트한다.  
기능, third-party services와의 통합, 모바일 또는 태블릿용 터치 입력과 같은 **유용성**을 확인한다.  
이미지의 대체 텍스트, 비디오의 폐쇄 자막(표시 여부를 선택할 수 있는 자막) 등의 **접근성**을 테스트 한다.  
[MDN Web Docs - Cross browser testing](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing#prerequisites)

<br/>

## 크로스 브라우징에 대한 오해

크로스브라우징은 완전한 동일성을 의미하는 것이 아니라 최소한 핵심 기능의 사용은 보장하는 동등성을 의미한다. 페이지가 완전히 똑같이 보이게 하는 것이 아님에 유의해야한다.  
예를 들어 동일한 페이지가 특정 브라우저에서 더 좋아 보일 수 있다. 하지만 정도의 차이가 있더라도 모든 브라우저에서 읽는 행위는 가능해야한다.

> ex - Modern Browser에서의 입체 애니메이션과, 구형 브라우저에서의 평면 그래픽.

<br/>

## Cross Browsing 을 위한 방법

1. 브라우저와 렌더링엔진의 점유율을 파악하고, 점유율이 높은 브라우저와 렌더링 엔진을 타겟팅하여 우선적으로 대응한다.
2. 사용하는 속성의 브라우저간 호환성을 확인한다.  
   [https://caniuse.com/](https://caniuse.com/) 등의 사이트에서 확인 가능하다.
3. Cross Browser Testing을 진행한다.  
   수동으로도 가능하지만, LambdaTest, CrossBrowserTesting.com 등의 온라인 사이트를 이용하는것이 편리하다.
4. **Reset.css**를 이용하여 CSS 초기화 작업을 수행한다.  
   `Reset.css`를 검색하면 많은 자료들이 나온다. Reset.css는 모든 속성에 대한 default 값을 한번씩 지정해서 브라우저마다 다른 기본 스타일 값을 초기화해주는 것이다. 그러면 모든 브라우저에서 동일한 스타일 결과를 기대할 수 있다.
5. Vender Prefix  
   CSS 속성 앞에 브라우저 별 접두사(Vender Prefix)를 붙이는 것이다. Vender Prefix는 과거 특정 브라우저에서만 지원되는 속성을 사용하기 위해 제공된 기능이다. 브라우저는 자신의 Vender Prefix가 붙은 속성을 인식하고 적용한다.  
   [autoprefixer.github.io/](autoprefixer.github.io/)는 접두사를 붙인 CSS를 생성해준다.

#### Vender Prefix와 사용 예

| prefix   | browser                                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| -webkit- | Chrome, Safari, 최신 버전의 Opera 및 Edge, iOS용 Firefox를 포함한 거의 모든 iOS 브라우저, 기본적으로 모든 WebKit 또는 Chromium 기반 브라우저 |
| -moz-    | Firefox                                                                                                                                      |
| -ms-     | IE                                                                                                                                           |
| -o-      | Opera의 WebKit 이전 버전                                                                                                                     |

<!-- prettier-ignore -->
```html
.button {
  -webkit-transition: all 4s ease;
  -moz-transition: all 4s ease;
  -ms-transition: all 4s ease;
  -o-transition: all 4s ease;
  transition: all 4s ease; //표준 속성
}
<!-- CSS는 순차적으로 적용되기 때문에 표준 속성을 마지막에 배치하는 것이 좋다. -->
<!-- 위의 예시는 최종적으로 transition: all 4s ease; 가 실행된다. -->
```

<br/>

## 브라우저 점유율

<div id="all-browser-ww-monthly-202111-202211" width="600" height="400">
  <img style="width:600px; height: 400px;" src="https://user-images.githubusercontent.com/66757141/206550905-14fc2633-181d-4229-b8b4-fa84f66f7b19.png" alt="StatCounter-browser-ww-monthly-202111-202211"/>
</div>
<p>Source: <a href="https://gs.statcounter.com/">StatCounter Global Stats - Browser Market Share</a></p>

Browser Market Share Worldwide - November 2022 를 참고하면 Chrome 이 65.84%로 가장 높았고 Safari 18.7%, Edge 4.44%가 뒤를 이었다.

<br/>

## 렌더링 엔진(레이아웃 엔진)

서로 다른 브라우저여도 동일한 렌더링 엔진을 사용한다면 비슷한 결과를 얻을 수 있다.

![화면 캡처 2022-12-09 041556](https://user-images.githubusercontent.com/66757141/206547114-5d26cf01-dfc0-4867-8641-3547e9e38570.png)
_Comparison of browser engines [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_browser_engines)_

**Active Status**는 새로운 웹 표준이 엔진에 추가되어 멀티미디어를 포함한 대다수의 웹사이트를 렌더링할 수 있음을 의미한다.  
**Maintained Status**는 적어도 엔진이 여전히 컴파일 됨을 의미한다.  
**Discontinued**는 엔진의 제공이 중단되었음을 의미한다.

- **Webkit** | 초기 애플사가 사파리 엔진으로 사용하기 위해 차용했으나 현재는 웹킷 프로젝트로 분리되어 개발되고 있다.  
  크롬에서도 사용되었던 엔진이며 iOS나 안드로이드의 기본 브라우저들이 이 웹킷 엔진을 사용한다.  
  점유율이 높은 엔진이다.
- **오페라**는 15버전부터 프레스토가 아닌 블링크를 사용했다.
- **듀얼 엔진** 국내 이스트소프트의 스윙(Swing) 브라우저를 예로 들면 크롬과 같은면서도 액티브X를 지원하는데, 독자적인 엔진이 아닌 두가지 엔진을 번갈아 사용하는 방식이기 때문에 가능하다. - 보통 트라이던트와 웹킷or블링크 엔진을 사용한다.

<br/>

---

## Reference

📄 https://blog.naver.com/insaweb/221926915225  
📄 https://github.com/Songwonseok/CS-Study/blob/main/Web/%ED%81%AC%EB%A1%9C%EC%8A%A4%20%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A7%95.md  
📄 https://mulder21c.github.io/2019/01/30/what-is-cross-browsing/
📄 https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix
