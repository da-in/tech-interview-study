# CSS(Cascading Style Sheets)

**CSS(Cascading Style Sheet)** 는 마크업 언어가 실제 표시되는 방법을 기술하는 스타일 언어(Style sheet language)로 HTML과 XHTML\* 에 주로 쓰이며, XML에서도 사용할 수 있다. W3C의 표준이고, 레이아웃과 스타일을 정의할 때의 자유도가 높다.

_\* XHTML(Extensible Hypertext Markup Language)은 HTML과 동등한 표현 능력을 지닌 XML 마크업 언어로, HTML보다 엄격한 문법을 가진다._

<br/>

## CSS Rule Set

**Rule Set** 은 어떤 요소에 어떤 스타일링을 할 것인지 브라우저에 알리는 하나의 CSS 문장으로 축약하여 **Set** 이라고도 한다. 말 그대로 Rule의 집합이다.

CSS Rule Set은 아래와 같은 형태를 갖는다.

<img src="https://user-images.githubusercontent.com/66757141/211836370-9f61a231-2988-42e0-8891-9bd827198877.png" alt="css rule set" width="500px" /><br/>
_[image reference](https://puzzleweb.ru/en/css/1_css_syntax.php)_

- **선택자(Selector)** : rule set의 맨 앞에 위치하는 HTML 요소 이름으로 꾸밀 요소를 선택한다.
- **선언(Declaration)** : 단일 규칙이다. 꾸미려는 속성과 값을 명시합니다.
- **속성(Property)** : 선택한 요소를 꾸밀 수 있는 방법이다. 예시에서는 color는 p 요소가 갖는 속성이다. rule 내에서 영향을 줄 속성을 선택한다.
- **값(Value)** : 주어진 속성이 가질 수 있는 형태의 값을 지정한다.

여러 Rule Set을 작성했을 때 Selector를 기준으로 구분하며, `{` , `}`로 감싸야한다. 각 선언을 구분하기 위해서 `;` 를 사용하고, 속성과 값은 `:`로 구분한다.

<br/>

## CSS의 작동

브라우저가 문서를 표시할 때, 문서의 콘텐츠와 해당 스타일 정보를 결합해야 한다. 그 과정을 단순화하면 아래와 같은 여러 단계를 거쳐 문서를 처리한다.

<img src="https://user-images.githubusercontent.com/66757141/211836326-4fb32b83-5d75-472c-b297-34fb9e44d32d.svg" alt="css works" width="600px" /><br/>
_[image reference](https://puzzleweb.ru/en/css/1_css_syntax.php)_

1. 브라우저가 `HTML`을 로드한다.
2. `HTML`을 접근 및 조작 가능한 형태인 문서 객체 모델 `DOM(Document Object Model)`으로 변환한다.
3. 브라우저는 HTML 문서에 연결된 이미지, 비디오 등의 리소스와 CSS를 가져온다.
4. 브라우저는 가져온 CSS를 구문 분석(parsing)하고 선택자 유형에 따른 각각의 규칙을 `buckets` 으로 정렬한다. 선택자를 기반으로 DOM 의 어느 노드에 어떤 규칙을 적용해야 하는지 확인한다.
   - CSSOM(Cascading Style Sheets Object Model) Tree를 생성한다.
5. DOM 트리에 스타일 정보를 첨부(Attach)하여 `Render Tree`를 생성한다. 따라서 `Render Tree`는 규칙이 적용된 후에 표시되어야 하는 구조로 배치됩니다.
6. 페이지의 시각적 표시가 화면에 표시(`Painting`)된다.

<img src="https://user-images.githubusercontent.com/66757141/211843953-026bdfd9-58f5-44a6-a7f2-b4a2e5971bd1.png" alt="dom, cssom, render tree" ><br/>
_[image reference](https://web.dev/critical-rendering-path-render-tree-construction/)_

<br/>

## CSS 명시도(Specificity)

**CSS 명시도(Specificity)** 는 동일한 요소 속성에 중첩하여 스타일을 선언하는 경우 어떠한 선언을 최종적으로 적용할지 **우선순위** 를 결정하는데 사용된다.

명시도는 CSS 선언(Declaration)에 적용되는 가중치(weight)로, 선언의 선택자가 갖는 **선택자 유형의 수** 에 의해 결정된다.

<br/>

### 선택자 유형

**유형 선택자(Type Selector)**

<!-- prettier-ignore -->
```css
a { color: red; }
```

**클래스 선택자(Class Selectors)**

<!-- prettier-ignore -->
```
<div class='class_value'>...<div>
.class_value { color: red; }
```

**ID 선택자(ID Selectors)**

<!-- prettier-ignore -->
```
<div id='id_value'>...<div>
#id_value { color: red; }
```

**특성 선택자(Attribute Selectors)**

<!-- prettier-ignore -->
```
a[href="https://example.org"] { color: red; }
```

**전체 선택자(Universal Selectors)**

```
* { color: red; }
* [lang^=en] { color: green; }
```

<br/>

### 명시도 산출

_https://specifishity.com/ 가중치를 확인할 수 있는 사이트라고 공식문서에 소개되어있는데 이게 뭐지 링크의 상태가 재미있다🤔_

가중치는 일반적으로 `X-Y-Z` 의 형태로 나타낸다.

- **X-0-0** : `ID Selectors` 의 수
- **0-Y-0** : `Class Selectors`, Attributes Selectors, Pseudo-Classes의 수
- **0-0-Z** : `Element(type) Selectors`와 Pseudo-elements의 수
- **1-0-0-0** : `인라인 스타일(inline style)`의 Rule은 더 큰 가중치를 갖는다.
- **1-0-0-0-0** : `!important`규칙을 사용하면 다른 선언보다도 우선시 된다.

```html
<!-- inline style -->
<div style="color: red;">Hello</div>
<!-- !important -->
.foo[style*="color: red"] { color: firebrick !important; }
```

_\*, \+, \>, ~ 등의 Universal Selector는 가중치를 증가시키지 않는다._

여러 선언의 명시도가 같은 경우 CSS에서 맨 끝에 오는, 즉 나중에 명시된 선언이 적용된다.  
명시도는 같은 요소가 여러 선언의 대상이 되는 경우에만 적용되며, CSS 규칙에 따라 부모로부터 상속받는 선언보다 요소를 직접 선택한 선언이 항상 우선된다.

<br/>

---

## Reference

📄https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/CSS_basics  
📄https://developer.mozilla.org/ko/docs/Web/CSS/Specificity  
📄https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/How_CSS_works  
📄https://ko.wikipedia.org/wiki/CSS

**브라우저 엔진을 직접 구현하며 원리를 설명하는 글**  
✨https://velog.io/@elrion018/브라우저-작동방식-탐구-CSS-파서Parser-구현하기
