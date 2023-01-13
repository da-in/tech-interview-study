# DOM (Document Object Model)
DOM은 XML이나 HTML 문서에 접근하기 위한 일종의 인터페이스이다. </br>
문서의 구조화된 표현을 제공해서 프로그래밍 언어가 DOM구조에 접근해 문서의 콘텐츠 및 구조, 그리고 스타일을 읽고 조작할 수 있도록 API를 제공한다.</br>
즉, 이를 통해 웹페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결 시켜주는 역할이다. </br>



## 웹 페이지 만드는 과정
- 브라우저가 HTML문서를 **파싱**하여 최종적으로 어떤 내용을 페이지에 렌더링 할지 결정 -> **렌더 트리**를 만든다!
   - 렌더 트리를 만들기 위해 `DOM`이 필요하다.
- 렌더 트리를 통해 브라우저가 **렌더링** 수행 </br>


> 파싱이란? - 텍스트 문자의 문자열을 토큰으로 분해하고, 문법적 의미와 구조를 반영해서 **Parse Tree**를 생성하는 과정 </br>
> 토큰이란? - 문법적으로 의미가 있는 최소 단위 </br>
> 렌더링이란? - `HTML, CSS`로 작성된 문서를 파싱하여 브라우저에 **시각적**으로 출력하는 것 </br>

<img src="https://user-images.githubusercontent.com/102718303/211845835-ee645f78-8ef6-4e9a-9e28-f58c72d30cf3.png">




## DOM의 구조
- DOM의 구조를 보면 단순 텍스트로 구성된 HTML 문서의 내용과 구조가 **객체 모델**로 변환되어 다양한 프로그램에서 사용 가능하다. </br>
- DOM의 개체 구조는 **트리 자료구조**로 표현된다.
- `<HTML>`은 **루트**, 그 안의 `Tag`들은 **자식**, 태그 안의 컨텐츠는 **잎**에 해당한다. </br>
- 이를 통해 자바 스크립트같은 언어를 이용해서 DOM에 접근해 수정할 수 있다. </br>

<img width="639" alt="HTML DOM" src="https://user-images.githubusercontent.com/102718303/211846015-15728956-d8ee-4fd8-882c-5414d53a5d4f.png">




## 구성요소
- `document node (문서 노드)`
    - DOM 트리에서 최상위 루트 노드이고, document 객체를 가리킨다.
    - `window.document`,`document` 로 참조해 사용 가능
    - HTML문서에 1개만 존재 
- `element node (요소 노드)`
    - 모든 태그들이 요소 노드이다.
    - 속성 노드를 가질 수 있는 유일 노드
- `attribute node (속성 노드)`
    - element node에 대한 정보를 가지고 있다. 
    - 부모 노드가 아닌 해당 노드와 연결되어 있다.
- `text node (텍스트 노드)`
    - 정보를 나타내는 노드 (리프 노드라고 하기도 한다,,)
</br>    
    
    
    
## 그럼 DOM이랑 HTML이랑 같나요?
DOM은 HTML이 아니다! 차이점들을 살펴보면
- 항상 유효한 HTML형식이다.
- `JavaScript`로 수정될 수 있는 동적 모델이다.
- 가상 요소를 포함하지 않는다.
> 가상요소란? - 선택한 요소의 일부에만 스타일을 적용하는 것 `::before, ::after`
- 보이지 않는 요소를 포함한다. 

</br>


## DOM에 접근하는 방법
- 단수 객체 접근 : `getElementByxx()`,`querySelector()` 사용
- 복수 객체 접근 : `getElements()`, `querySelctorAll()` 사용

1개의 DOM 요소는 `Tagname`, `ID`, `Classname`, `CSSSelector`를 통해 접근할 수 있다.

```
// TagName으로 찾기
document.getElementsByTagName('input') 

// ID로 찾기
document.getElementsById('search')

// ClassName으로 찾기
document.getElementsByClassName('search-input-style')

// CSSSeletor로 찾기
document.querySelector('.search-input-style')
```
</br>



## 주요 DataTypes
|||
|------|----------|
|document|menber가 document type의 객체를 리턴할 때, 이 객체는 root document object 자체이다. 예를들어 `document.getElementById("myP").ownerDocument`는 해당 프로퍼티가 속해 있는 document를 리턴한다.|
|element|element는 DOM API의 member에 의해 리턴된 element 또는 element type의 node를 의미한다. 즉 `document.createElement()` 메소드가 DOM안에서 생성되는 element를 리턴한다고 할 수 있다.|
|nodeList|nodeList는 elements의 배열이다.(`document.getElementsByTagName()`의 리턴 값과 같다) nodeList의 item은 인덱스를 통해 접근 가능하다. |
|attribute|attribute가 member에 의해 리턴되는 것은 attribute에 대한 인터페이스를 노출하는 Object reference이다. 쉽게 말하면 attribute는 elements와 같은 노드이다.(`createAttiribute()`) |
|namedNodeMap|nameNodeMap은 배열과 유사하지만 각 item은 name이나 인덱스에 의해 접근할 수 있다. nameNodeMap은 item() 메소드가 있고, item을 추가/삭제할 수 있다.|


> member란? - 프로퍼티 혹은 메소드 </br>
> 프로퍼티란? - DOM 객체의 멤버 변수이고,  HTML 태그의 속성을 반영</br>
> 메소드란? - DOM 객체의 멤버 함수이고, HTML 태그를 제어</br>

</br>

## DOM 사용예시 (JavaScript)

```JavaScript
<script type="text/javascript">
	window.onload = function() {
		var header = document.createElement('p');
		var textNode = document.createTextNode('이것이 DOM이다.');
		header.appendChild(textNode);
		document.body.appendChild(header);
	};
</script>
```
1. document 객체에 접근해서 `p` 태그를 생성
2. document 객체에 다시 접근해서 TextNode를 생성 후 String을 삽입
3. appendChil 메소드로 textNode를 자식노드로 추가
4. document 객체에 있는 `body` 태그에 header를 자식노드로 추가

> JavaScript와 DOM은 엄밀히 다른 개념이다! -> 다른 언어로도 DOM을 다룰 수 있다. </br>
> 현재 웹 브라우저에서 DOM을 조작하는 언어는 JavaScript뿐,, </br>


</br>

## 인터페이스와 객체
- 많은 객체들이 여러개의 다른 인터페이스들과 연관되어 있다.
	- 예를들어, table객체는 여러 메소드들이 포함된 `HTMLTableElement`를 구현함과 동시에 `HTML Element`이기도 하기 때문에 `Element` 인터페이스도 구현한다. 

</br>


## DOM의 핵심 인터페이스
- `document.getElementById(id)`
- `document.getElementsByTagName(name)`
- `document.createElement(name)`
- `parentNode.appendChild(node)`
- `element.innerHTML`
- `element.setAttribute`
- `element.getAttribute`

----
## Referance
- http://www.tcpschool.com/javascript/js_dom_concept
- https://wit.nts-corp.com/2019/02/14/5522
- https://velog.io/@sj_dev_js/HTML-DOM%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C
- https://www.codestates.com/blog/content/dom-javascript
- https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction
