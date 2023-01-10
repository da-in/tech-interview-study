# CORS(Cross-Origin Resource Sharing)

웹 개발을 하다보면 CORS 문제를 종종 볼 수 있다. 에러 메세지를 보면 **CORS policy** 에 의해 요청이 Block 되었다는 내용이다. CORS에 대하여 알아본다.

<img width="550" alt="redscreenshot" src="https://user-images.githubusercontent.com/66757141/211569746-a89112d7-bb30-4945-a84a-f2b8243f6ebd.png"><br/>
_[image reference](https://blog.container-solutions.com/a-guide-to-solving-those-mystifying-cors-issues)_

<br/>

## CORS

> **CORS(Cross-Origin Resource Sharing)** 는 HTTP 헤더를 전송하는 시스템으로, 프론트엔드 자바스크립트 코드가 교차-출처 요청(cross-origin request)에 대한 응답에 접근하는 것을 브라우저가 차단하는지 여부를 결정한다. [CORS-MDN](https://developer.mozilla.org/en-US/docs/Glossary/CORS)

CORS(Cross-Origin Resource Sharing)는 직역하면 교차-출처 리소스 공유이다. 출처가 다른 자원들에 접근하도록 하는 개념이다.

**동일-출처 보안 정책(same-origin security policy)** 는 교차-출처 접근을 제한한다. 이 때 CORS는 웹 서버가 교차-출처 접근을 선택적으로 허용할 수 있도록 해준다.

<br/>

## 출처(Origin)

_[image reference](https://subscription.packtpub.com/book/cloud-and-networking/9781789349863/6/ch06lvl1sec60/what-s-in-a-url)_

동일한 출처란 `protocol`, `port`, `host`가 동일한 URL을 말한다.
`http://store.company.com/dir/page.html`와 아래 URL들이 동일한 출처인지 확인해본다.

<!-- prettier-ignore -->
| URL | 결과 | 이유 |
| --- | ---- | ---- |
| `http://store.company.com/dir2/other.html` | Same origin | `path`만 다르다 |
| `https://store.company.com/page.html` | Failure | `protocol`이 다르다 |
| `http://store.company.com:81/dir/page.html` | Failure | `port`가 다르다 |
| `http://news.company.com/dir/page.html` | Failure | `host`가 다르다 |

---

## Reference

📄https://developer.mozilla.org/ko/docs/Glossary/CORS  
📄https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy  
📄https://escapefromcoding.tistory.com/724
