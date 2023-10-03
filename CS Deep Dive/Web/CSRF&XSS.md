# CSRF & XSS
보안 공격에는 `Click-jaking`, `XSS`, `CSRF`, `MitM`, `Session hijacking`등의 다양한 유형이 존재하는데, 그 중 `CSRF`와 `XSS`공격에 대하여 다룬다. 모든 공격에 대한 내용은 [MDN | Types of attacks
](https://developer.mozilla.org/ko/docs/Web/Security/Types_of_attacks)에 자세히 나와있다.

## CSRF(Cross Site Request Forgery)
`CSRF`는 웹사이트 취약점 공격 유형 중 하나로 `XSRF`라고도 한다. 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(`modify`, `delete`, `register` 등)를 특정한 웹사이트에 `request`하도록 만드는 공격이다. 해커가 사용자의 SNS 계정으로 광고성 글을 올리는 것은 대표적인 CSRF 공격에 해당한다.

### CSRF 공격 흐름
1. 사용자는 웹사이트에 로그인하여 정상적인 [쿠키](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Web/Cookie%26Session.md)를 발급받는다.
2. 공격자는 공격용 HTML 페이지 링크를 이메일이나 게시판 등을 통해 사용자에게 전달한다.
3. 공격용 HTML 페이지는 다음과 같은 이미지 태그를 가진다.  
   ```html
   <img src="https://bank.example.com/withdraw?account=bob&amount=1000000&for=mallory" />
   ```
4. 사용자가 공격용 페이지를 로드하면, 브라우저는 이미지 파일을 받아오기 위해 `src` 속성으로 등록되어있는 URL에 요청을 보낸다.
5. 로그인 상태로 쿠키가 유효하고 다른 확인이 없는 경우, 사용자의 승인이나 인지 없이 송금되어 공격이 완료된다.

> `POST`메서드의 엔드포인트도 보이지 않는 `<form>` 제출을 트리거하는 방법으로 공격할 수 있다.

### CSRF 대응 방법

**리퍼러(Referer) 검증**  
백엔드에서 Referer\* 검증을 통해 승인된 도메인으로 요청시에만 처리하도록 한다.

\* referer : `HTTP request header`에 포함된 요청을 보낸 웹 페이지의 주소

**CSRF Token 사용**  
사용자의 세션에 임의의 난수 값을 저장하고, 사용자의 요청시 해당 값을 포함하여 전송시킨다. 백엔드에서는 요청을 받을 때 세션에 저장된 토큰값과 요청 파라미터로 전달받는 토큰 값이 일치하는 지 검증 과정을 거치는 방법이다.

<br/>

## XSS(Cross Site Scripting)

`XSS`는 `CSRF`와 같이 웹사이트 취약점 공격 유형 중 하나로, 관리자가 아닌 권한이 없는 사용자가 웹 사이트에 스크립트를 삽입하는 공격 기법이다.
- 이를 통해 사용자의 정보(쿠키, 세션 등)을 탈취하거나, 자동으로 비정상적인 기능을 수행할 수 있다.
- 주로 다른 웹사이트와 정보를 교환하는 식으로 작동하므로 사이트 간 스크립팅이라고 한다.
- `CSS`라는 이름은 웹 기술인 `CSS`와 중복되어 `XSS`라고 부른다.

### XSS 공격 유형

`XSS`공격의 세부 유형은 표준으로 정해져 있지 않지만, 일반적으로 `반사형(Non-persistent)`, `저장형(persistent)`, `DOM 기반 XSS` 등으로 구분한다.

**반사형(Reflected, Non-persistent)**  
반사형 XSS 공격은 요청 메세지에 입력된 스크립트 코드가 즉시 응답 메세지를 통해 출력되는 취약점을 이용한다. 공격자가 주입한 스크립트가 브라우저에 반사되는 것처럼 동작하여 붙은 이름이다.

**저장형(Stored, Persistent)**  
악성 스크립트를 대상 서버에 삽입하여 이를 열람한 사용자를 공격 한다. 삽입된 스크립트를 서버에 저장시켜 지속적으로 공격을 하기 때문에 `Persistent XSS`라고 불린다.

**DOM 기반**  
악성 스크립트가 포함된 URL을 사용자가 요청하게 되면서 브라우저를 해석하는 단계에서 발생하는 공격이다. 이 스크립트로 인해 클라이언트 측 코드가 원래 의도와 다르게 실행된다. 이는 다른 XSS 공격과는 달리 서버 측에서 탐지가 어렵다.

### XSS 대응 방법

**입력 값 검증**  
데이터가 입력되기 전이나, 서버에 전달하기 전 검증하는 방식으로, 입력 데이터 길이 제한, 특정 값 무효화 등을 수행할 수 있다.

**출력 값 검증**
출력하려는 데이터에 스크립트로 해석될 여지가 있는 문자열을 인코딩하는 것이다. `<`를 `&lt;`, `>`를 `&gt;`로 변환하는 등의 과정을 거쳐 출력하면 스크립트로 해석되지 않는다.

**보안 라이브러리 사용**    
Anti XSS 라이브러리를 제공해주는 회사들이 많다. 서버 단에서는 이러한 라이브러리들을 추가하여, 클라이언트는 브라우저에 확장앱을 설치하여 방어할 수 있다.

<br/>

---
## Reference
📄https://developer.mozilla.org/ko/docs/Web/Security/Types_of_attacks  
📄https://ko.wikipedia.org/wiki/사이트_간_요청_위조  
📄https://itstory.tk/entry/CSRF-공격이란-그리고-CSRF-방어-방법  
📄https://noirstar.tistory.com/266
