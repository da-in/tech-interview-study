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

---

## Reference

📄https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/CSS_basics  
📄https://ko.wikipedia.org/wiki/CSS

**브라우저 엔진을 직접 구현하며 원리를 설명하는 글**  
✨https://velog.io/@elrion018/브라우저-작동방식-탐구-CSS-파서Parser-구현하기
