# HTTP Request Method

자원의 표현에 의한 상태 전달의 개념을 이해하기 위해 [REST API](https://github.com/da-in/tech-interview-study/blob/main/CS%20Deep%20Dive/Web/REST%20API.md)를 선행하여 읽어보면 좋다.

> HTTP는 주어진 **자원**에 대해 수행하고자 하는 동작을 나타내기 위한 `Request Method`를 정의한다. 간혹 `Request Method`를 "HTTP 동사"라고 부르기도 한다. 각각의 메서드는 서로 다른 의미를 구현하지만, 각 메서드 간에 일부 공통적인 특징을 갖기도 한다. 이를테면 응답 메서드는 안전하거나, 캐시 가능하거나, 멱등성\*을 가질 수 있다. [MDN Web Docs - HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

_\* 멱등성(idempotent) : 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질_

<br/>

## HTTP Request Method

자주 사용되는 메서드로는 `GET`, `POST`, `PUT`, `PATCH`, `DELETE` 등이 있으며, 그 외에도 다양한 메서드들이 있다.

#### 1. GET

`GET` 메서드는 지정된 리소스의 표현을 요청한다. `GET`을 사용하는 요청은 데이터를 검색하기만 해야한다. 쉽게 말해, 원하는 정보를 서버에 요청할 때 쓰이며, 리소스의 위치를 URL의 Query String 등으로 표현하기 때문에 일반적으로 `RequestBody`가 없다.

#### 2. HEAD

`HEAD`는 동일한 Request URL을 `GET`으로 보냈을 때 오는 응답의 헤더를 요청하는 메서드이다. 쉽게 말해 `GET`과 동일한데 `Response Body`가 없는 것이다.

예를 들어, URL에서 대용량 다운로드가 발생할 수 있는 경우 `HEAD` 요청은 파일을 실제로 다운로드하지 않고 파일 크기를 확인하기 위해 해당 `Content-Length` 헤더를 읽을 수 있다.

#### 3. POST

자원을 생성하기 위해 사용되는 메소드이다. 반복해서 호출했을 때에는 반복해서 요소를 생성하므로 멱등\*하지 않다. POST로 정보를 전송하면 URL에 파라미터가 나타나지 않으므로 각종 데이터를 전송하는데에도 쓰인다.

#### 4. PUT

`PUT` 메서드는 새 리소스를 생성하거나 대상 리소스의 표현을 대체할 때 사용한다. URI의 자원이 이미 존재할 경우 요청한 요소로 대체하고, 존재하지 않을 경우에는 자원을 새로 생성한다.

`PUT`과 `POST`의 차이점은 PUT가 멱등\*하다는 것이다. PUT은 여러 번 연속적으로 호출했을 때 동일한 효과(부작용이 없음)인 반면, POST는 연속적으로 호출했을 때 사이드 이펙트가 발생할 수 있다.

#### 5. PATCH

요청된 자원을 수정하기 위해 사용되는 메서드라는 점은 `PUT`과 같지만, 해당 자원 전체를 수정하는 `PUT`과는 다르게 `PATCH`는 해당 자원의 일부분을 수정한다.

#### 6. DELETE

자원을 삭제하기 위한 메서드이다. 서버 내 보안규칙 없이 클라이언트에서 서버의 자원을 삭제할 수 있도록 허가하는 것은 매우 위험하다.

#### 7. TRACE

`TRACE`는 루프백 메시지를 호출하기 위해 테스트 목적으로 사용되는 메소드이다. 클라이언트의 요청이 서버에 도달했을 때 어떻게 보이는지 보여주어 디버깅에 사용한다.

#### 8. OPTION

웹서버에서 지원하는 메서드를 알기 위해 사용되는 메소드이다. 특정 자원에 대해 허용되는 메서드를 알 수 있다.

#### 9. CONNECT

`CONNECT` 메서드는 요청된 리소스와 양방향 통신을 시작하도록 한다. 터널을 여는 데 사용할 수 있다.

<br>

## GET / POST

가장 높은 빈도로 사용되고, 자주 비교되는 두 메서드 `GET`과 `POST`메서드의 차이점을 정리한다.

#### GET

`GET`은 지정된 리소스에 데이터를 요청하는 데 사용된다.  
`Query String`(이름/값 쌍)은 GET 요청의 URL로 다음과 같이 전송된다.

```
/test/demo_form.php?name1=value1&name2=value2
```

- `GET` 요청은 캐시할 수 있다.
- `GET` 요청은 브라우저 기록에 남는다. (요청 정보가 URL에 포함되기 때문이다.)
- `GET` 요청을 북마크할 수 있다.
- 중요한 데이터를 처리할 때 `GET` 요청을 사용해서는 안 된다.
- `GET` 요청에는 길이 제한이 있다.
- `GET` 요청은 데이터를 요청하는 데만 사용된다.(수정하지 않음)

#### POST

`POST`는 서버에 데이터를 전송하여 리소스를 생성/업데이트하는 데 사용된다.  
`POST`와 함께 서버로 전송된 데이터는 HTTP 요청의 요청 본문에 다음과 같이 저장된다.

```
POST /test/demo_form.php HTTP/1.1
Host: w3schools.com

name1=value1&name2=value2
```

- `POST` 요청은 일반적으로 캐시되지 않는다. (단, 캐싱 정책에 의해 유효한 정보가 포함될 경우에는 가능)
- `POST` 요청은 브라우저 기록에 남지 않는다.
- `POST` 요청은 북마크할 수 없다.
- `POST` 요청은 데이터 길이에 제한이 없다.

<br>

---

## Reference

📄 https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods  
📄 https://www.w3schools.com/tags/ref_httpmethods.asp  
📄 https://gnaseel.tistory.com/24  
📄 https://dev-coco.tistory.com/161
