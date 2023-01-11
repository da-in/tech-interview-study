# DOM (Document Object Model)
DOM은 XML이나 HTML 문서에 접근하기 위한 일종의 인터페이스이다. </br>
문서의 구조화된 표현을 제공해서 프로그래밍 언어가 DOM구조에 접근하여 문서의 콘텐츠 및 구조, 그리고 스타일을 읽고 조작할 수 있도록 API를 제공한다.</br>
즉, 이를 통해 웹페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜준다.


### 웹 파이지 만드는 과정
- 브라우저가 HTML문서를 파싱하여 최종적으로 어떤 내용을 페이지에 렌더링 할지 결정 -> 렌더트리를 만든다!
   - 렌더 트리를 만들기 위해 `DOM`이 필요하다.
- 렌더트리를 통해 브라우저가 렌더링 수행

> 파싱이란? - 텍스트 문자의 문자열을 토큰으로 분해하고, 문법적 의미와 구조를 반영해서 Parse Tree를 생성하는 과정 </br>
> 토큰이란? - 문법적으로 의미가 있는 최소 단위 </br>
> 렌더링이란? - `HTML, CSS`로 작성된 문서를 파싱하여 브라우저에 **시각적**으로 출력하는 것 </br>

<img src="https://user-images.githubusercontent.com/102718303/211845835-ee645f78-8ef6-4e9a-9e28-f58c72d30cf3.png">


## DOM의 구조
HTML DOM의 구조를 보면 단순 텍스트로 구성된 HTML 문서의 내용과 구조가 객체 모델로 변환되어 다양한 프로그램에서 사용 가능하다. </br>
따라서 DOM의 개체 구조는 **트리 자료구조**로 표현된다.
> `<HTML>`은 **루트**, 그 안의 `Tag`들은 **자식**, 태그 안의 컨텐츠는 **잎**에 해당한다. </br>

이를 통해 자바 스크립트같은 언어를 이용해서 DOM을 수정할 수 있다. </br>

<img width="639" alt="HTML DOM" src="https://user-images.githubusercontent.com/102718303/211846015-15728956-d8ee-4fd8-882c-5414d53a5d4f.png">


----
## Referance
- http://www.tcpschool.com/javascript/js_dom_concept
- https://wit.nts-corp.com/2019/02/14/5522
- https://velog.io/@sj_dev_js/HTML-DOM%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C
