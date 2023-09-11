# CORS(Cross-Origin Resource Sharing)

웹 개발을 하다보면 CORS 문제를 종종 볼 수 있다. 에러 메세지를 보면 **CORS policy** 에 의해 요청이 Block 되었다는 내용이다. CORS에 대하여 알아본다.

<img width="550" alt="redscreenshot" src="https://user-images.githubusercontent.com/66757141/211569746-a89112d7-bb30-4945-a84a-f2b8243f6ebd.png"><br/>
_[image reference](https://blog.container-solutions.com/a-guide-to-solving-those-mystifying-cors-issues)_

<br/>

## CORS

> **CORS(Cross-Origin Resource Sharing)** 는 HTTP 헤더를 전송하는 시스템으로, 프론트엔드 자바스크립트 코드가 교차-출처 요청(cross-origin request)에 대한 응답에 접근하는 것을 브라우저가 차단하는지 여부를 결정한다. [CORS-MDN](https://developer.mozilla.org/en-US/docs/Glossary/CORS)

CORS(Cross-Origin Resource Sharing)는 직역하면 교차-출처 리소스 공유이다. 출처가 다른 자원들에 접근하도록 하는 개념이다.

**동일-출처 보안 정책(same-origin policy, SOP)** 는 교차-출처 접근을 제한한다. 이 때 CORS는 웹 서버가 교차-출처 접근을 선택적으로 허용할 수 있도록 해준다.

<br/>

## 출처(Origin)

동일한 출처란 `protocol`, `port`, `host`가 동일한 URL을 말한다.

<img src="https://user-images.githubusercontent.com/66757141/211576962-20aee656-5bff-48d5-8de2-c541e8c87048.png" alt="71d250c0-2b41-43b9-8579-0f129e115bc8" width="450px" /><br/>
_[image reference](https://subscription.packtpub.com/book/cloud-and-networking/9781789349863/6/ch06lvl1sec60/what-s-in-a-url)_

### 동일 출처 예시

`http://store.company.com/dir/page.html`와 아래 URL들이 동일한 출처인지 확인해본다.

<!-- prettier-ignore -->
| URL | 결과 | 이유 |
| --- | ---- | ---- |
| `http://store.company.com/dir2/other.html` | Same origin | `path`만 다르다 |
| `https://store.company.com/page.html` | Failure | `protocol`이 다르다 |
| `http://store.company.com:81/dir/page.html` | Failure | `port`가 다르다 |
| `http://news.company.com/dir/page.html` | Failure | `host`가 다르다 |

<br/>

## 동일-출처 정책(same-origin policy, SOP)

다른 출처의 요청에 대한 제약이 존재하지 않는다면 `CSRF(Cross-Site Request Forgery)`나 `XSS(Cross-Site Scripting)`공격을 사용해서 정보를 탈취하고 서버에 요청을 보낼 것이다. 동일-출처 정책(SOP)은 다른 출처에서의 접근을 브라우저단에서 차단하여 위와 같은 상황을 방지한다.  
_출처를 비교하여 차단하는 로직은 서버가 아닌 브라우저에 구현되어있다. 그래서 브라우저가 아닌 서버간의 통신 등에는 CORS로부터 자유롭다._

하지만 다른 출처의 리소스 요청이 필요할 경우가 있다. 이 경우 CORS 정책을 준수하여 요청해야 정상적으로 응답을 받을 수 있다.

_\+ `<img>`, `<video>`, `<object>`, `<embed>`, `@font-face`, `<iframe>` 는 기본적으로 Cross Origin Policy를 지원한다_

<img src="https://user-images.githubusercontent.com/66757141/211583854-6fe49229-7a6a-4b9f-8c3c-60e622a7161f.png" alt="cors_principle" width="500px" /><br/>
_[image reference](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)_

<br/>

## CORS 기본 동작

1. Client가 HTTP Request Header에 `Origin` 필드로 출처를 담아 보낸다.

   ```
   Origin: http://localhost:3000
   ```

2. Server가 Response Header에 `Access-Control-Allow-Origin` 필드에 접근이 허용된 출처를 담아 보낸다.
   ```
   Access-Control-Allow-Origin: http://localhost:3000
   ```
3. Client에서 보냈던 `Origin`과 서버가 응답한 `Access-Control-Allow-Origin`를 비교해서 유효하다면 문제없이 응답을 가져온다. 만약 출처가 유효하지 않다면 해당 응답을 버리게되고, CORS 에러가 발생한다.

앞서 출처를 비교하여 차단하는 로직은 서버가 아닌 브라우저에 구현되어있다고 했지만, 결과적으로 CORS 허용을 위해서는 서버가 `Access-Control-Allow-Origin`에 사용하고자 하는 출처를 기재하여 응답해야한다. 때문에 CORS 에러가 발생했을 경우 백엔드 개발자가 수정해주어야하는 경우가 많다.

<br/>

## CORS의 세 가지 시나리오

위의 설명은 CORS의 기본적인 흐름이로, 실제로 CORS는 상황에 따른 세 가지 구체적인 시나리오를 갖는다. 각 시나리오의 자세한 내용은 [MDN - CORS#functional_overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#functional_overview) 에서 확인할 수 있다.

### Simple Request

첫 번째는 `단순 요청(Simple Request)`이다. 아래의 예비 요청을 보내지 않고 바로 본 요청을 보내어, 위의 기본 흐름과 같이 동작한다. Simple Request는 예비 요청 없이 바로 본 요청을 보내기에, 안전하다고 판단되는 아래의 조건들을 만족하는 경우에만 가능하다.

1.  HTTP `GET`, `HEAD`, `POST` 메소드를 사용해야한다.
2.  `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, `DPR`, `Downlink`, `Save-Data`, `Viewport-Width`, `Width` 헤더일 경우 에만 적용된다.
3.  Content-Type 헤더가 `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`중 하나여야한다.

대부분의 API 요청이 `text/xml`, `application/json` Content-Type을 갖는 등 사실상 위 조건을 만족하는 경우가 많지 않기에 대부분의 경우 예비 요청을 보내어 안전성을 확인한다.

<br/>

### Preflight Request

브라우저가 요청을 보내기 전 스스로 안전한 요청인지를 확인하기 위해 `예비 요청(Preflight Request)`을 보내는 경우이다. 예비 요청은 `OPTIONS` HTTP 메소드를 사용한다.

1. Client가 CORS 요청을 보내려고 한다.
2. Client가 본 요청 전 HTTP `OPTIONS` 메소드로 예비 요청을 보낸다.
   - `Origin` : 자신의 출처를 넣는다.
   - `Access-Control-Request-Method` : 실제 요청에 사용할 메소드
   - `Access-Control-Request-Headers` : 실제 요청에 사용할 헤더
3. Server는 Preflight에 대한 응답으로 CORS 허용과 금지에 대한 헤더 정보를 담는다.
   - `Access-Control-Allow-Origin` : 허용되는 Origin들의 목록
   - `Access-Control-Allow-Methods` : 허용되는 메소드 목록
   - `Access-Control-Allow-Headers` : 허용되는 헤더 목록
   - `Access-Control-Max-Age` : 해당 예비 요청의 초단위 브라우저 캐싱 시간
4. 요청과 응답 정책을 확인하여 안전하면 본 요청을 보낸다.

<br/>
<img src="https://user-images.githubusercontent.com/66757141/211611529-a81dba8b-5da6-46c2-ab01-e214afd68876.png" alt="1920px-Flowchart_showing_Simple_and_Preflight_XHR svg" width="800px" /><br/>

<!-- prettier-ignore -->
_[image reference](https://ko.wikipedia.org/wiki/%EA%B5%90%EC%B0%A8_%EC%B6%9C%EC%B2%98*%EB%A6%AC%EC%86%8C%EC%8A%A4*%EA%B3%B5%EC%9C%A0) 브라우저가 Simple Request를 보낼지 Preflight Request를 보낼지 결정하는 방식 플로우차트_

<br/>

### Credentialed Request

Client가 보내려는 요청에 `자격 인증 정보(Credential)`이 담겨있는 경우 위의 두 시나리오와는 다른 `인증된 요청(Credentialed Request)`을 전송한다.

_\* 자격 인증 정보는 세션 Id가 담긴 쿠키(Cookie), Authorization 헤더의 토큰 값 등을 말한다._

1. Client가 Request에 Credential 옵션을 설정한다.
   ```js
   credentials: 'include',
   ```
   - `same-origin(default)` : 같은 출처의 요청에만 인증 정보를 담을 수 있다.
   - `include` : 인증 정보를 담는다.
   - `omit` : 인증 정보를 담지 않는다.
2. Server가 인증된 요청에 대한 응답 헤더를 설정한다.
   - `Access-Control-Allow-Credentials`을 `true`로 설정한다.
   - `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`에 와일드카드 문자" \* "를 사용할 수 없다.

<br>

---

## Reference

📄https://developer.mozilla.org/ko/docs/Glossary/CORS  
📄https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy  
📄https://escapefromcoding.tistory.com/724  
📄https://inpa.tistory.com/entry/WEB-📚-CORS-💯-정리-해결-방법-👏
