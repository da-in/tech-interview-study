# JWT(JSON Web Token)

## JWT 개념

> [jwt.io introduction](https://jwt.io/introduction) | JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

JWT는 사용자 인증을 위해 사용하는 open standard(RFC 7519)\*이다.  
**Json 포맷으로 사용자의 정보 자체를 토큰으로 사용하는 Self-Contained 방식의 Claim 기반 Web 토큰이다.**

_\* open standard : 개방형 표준(일반적으로 사용하는데 로열티가 없음)_  
_\* RFC : 미국의 국제 인터넷 표준화기구 IETF(Internet Engineering Task Force)에서 관리하는 문서._

<br/>

## Claim 기반의 토큰

Claim은 사용자에 대한 프로퍼티나 속성을 말한다. JWT는 Claim을 JSON으로 정의하여 토큰에 직접 사용한다. 다음은 JSON으로 서술한 Claim의 예 이다.

```JSON
{
  "id": "dain",
  "role": ["admin", "user"],
  "team": "roundshoulder"
}
```

이러한 Claim 기반의 토큰을 사용하면 토큰 내에 담겨있는 정보를 얻기 위하여 추가적인 요청을 하지 않아도 된다는 장점이 있다.

Claim 방식이 아닌 OAuth의 access_token은 random string으로 토큰에 정보가 담겨있지 않다. 토큰에 관한 정보를 서버측에 별도로 저장해두고, 클라이언트에서 API 요청이 있을 경우 access_token으로 해당 토큰의 권한이나 정보를 확인하게 된다.

반면에 Claim 기반의 JWT는 토큰에 관한 정보를 서버에 저장하지 않는다. 토큰과 관련된 사용자 권한과 정보를 토큰 자체에 넣어 사용하기 때문에, 클라이언트와 서버에서는 토큰을 읽음으로서 권한과 정보를 확인할 수 있다.

_\* JWT 이전에 XML 기반의 SAML 2.0 토큰이 유사한 방식을 사용하였으나, 사이즈가 커서 API 요청시 HTTP 헤더에 담겨 전송될 경우 파싱에 대한 오버헤드가 발생하였다. 또한 JSON에 비하여 데이터 파싱과 사용이 어려웠다._

<br/>

## JWT 구조

JWT는 `Header`, `Payload`, `Signature` 세 부분으로 이루어져있다.

각 부분은 JSON 형태의 Claim에 기반하는데, "\n" 의 개행문자를 포함하기 때문에 Header 등에 삽입하기에 불편하다. 그래서 JWT는 JSON 형태의 Claim을 BASE 64 인코딩을 통하여 문자열로 변환한다.

JWT는 세 부분의 인코딩된 문자열을 `.`으로 연결한 형태이다.

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ImRhaW4iLCJyb2xlIjpbImFkbWluIiwidXNlciJdLCJ0ZWFtIjoicm91bmRzaG91bGRlciJ9.lhMolD40R2Lk1moWcUP_AHQ3BpF1hdB-eMWFljZaVzI
```

![사진]()

[JWT Online Debugger (jwt.io)](https://jwt.io/) 를 통해 위 JWT 토큰을 확인하면 아래와 같이 내용을 확인할 수 있다. BASE64Url은 암호화가 아닌 단순 인코딩이기 때문에 동일한 정보에 대하여 항상 동일한 문자열을 반환한다.

#### Header

Header는 `typ`와 `alg` 두 가지 정보로 구성된다.
typ는 토큰의 타입을 의미한다.
alg는 뒤에서 나오는 Signiture의 해싱 알고리즘을 지정한다.

```JSON
{
  "alg": "HS256",
  "typ": "JWT"
}
```

#### Payload

Payload 에는 정보인 Claim 들이 담겨있으며, Claim은 3가지로 분류된다.

1. 등록된 클레임(Registered Claim)  
    사전에 정의되어있는 정보들로, 선택해서 사용이 가능하지만 강력하게 사용 권고된다.
   ```JSON
   {
      "iss": "토큰 발급자(issuer)",
      "sub": "토큰 제목(subject)",
      "aud": "토큰 대상(audience)",
      "exp": "토큰 만료 시간(expiration)",
      "nbf": "토큰 활성 날짜(not before)",
      "iat": "토큰 발급 시간(issued at)",
      "jti": "JWT 토큰 식별자(JWT ID)",
   }
   ```
2. 공개 클레임(Public Claim)  
   사용자 정의 클레임으로, 임의로 사용할 수 있으나 충돌 방지(서로 다른 기대값을 방지 및 호환)를 위해서는 [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml)에 정의된 형태를 사용하거나, URI 형태로 정의해야한다.

3. 비공개 클레임(Private Claim)  
   사용자 정의 클레임으로, 통신을 주고받는 당사자간 협의 하에 정한 키와 값.

#### Signature

Signature는 토큰의 유효성 검증을 할 때 사용하는 고유한 암호화 코드이다. Header와 Payload의 BASE64Url로 인코딩한 값을 비밀 키를 이용해 Header에서 정의한 알고리즘(alg)으로 해싱을 하고 이를 다시 BASE64Url로 인코딩하여 생성한다.

<br/>

## JWT의 사용

사용자가 로그인을 성공하면 서버에서 JWT 토큰을 발급해준다.

클라이언트는 HTTP 통신시 발급한 JWT를 Request 헤더의 `Authorization`키의 값으로 지정한다.
일반적으로 앞에 Bearer Prefix\*를 붙인다.

_\* Authorization의 value는 인증 타입을 구분하기 위한 prefix를 앞에 붙이도록 HTTP 1.0 spec에 명시되어있다. Bearer 인증 토큰에 관한 내용은 [OAuth 2.0 authorization standard](https://datatracker.ietf.org/doc/html/rfc6750) 에서 확인할 수 있고, 그 외에도 Basic, Digest 등의 타입이 있다._

```JSON
{
    "Authorization": "Bearer {TOKEN}",
}
```

서버는 API Request Header의 토큰을 통해 사용자를 확인하고 응답한다.

<br/>

## JWT의 장단점

#### 장점

1. Header와 Payload를 함께 해싱하여 Signature를 생성하므로 `데이터 위변조`를 막을 수 있다.
2. `Self-contained` 방식으로 필요한 모든 정보를 자체적으로 지니고 있다.
3. 클라이언트 인증 정보를 저장하는 세션과 다르게, 서버는 무상태(StateLess)로 인증 정보에 대한 별도의 저장소를 사용하지 않고, 서버 확장성이 증가할 수 있다.
4. 쿠키와는 다르게 토큰 기반으로 다른 로그인 시스템 접근 및 권한 공유가 가능하다.
5. OAuth의 경우 Facebook, Google 등 소셜 계정을 이용하여 다른 웹서비스에서도 로그인을 할 수 있다.
6. 세션 사용이 불가능한 모바일 앱에서도 동작한다.

#### 단점

1. 토큰 자체에 정보를 담고 있는 `Self-contained` 방식이고, Payload가 암호화가 아닌 Base 64 인코딩 된 것이기 때문에 탈취하여 복호화하면 데이터를 볼 수 있다.(따라서 Payload에는 중요한 데이터를 담지 않아야 한다.)
2. Payload의 클레임이 많아질수록 `토큰의 길이`가 늘어나 부하를 줄 수 있다.
3. `stateless` 특징으로 토큰의 정보가 서버에 저장되지 않고 클라이언트 측에서 관리 및 저장하여 사용한다. 때문에 토큰을 탈취당하면 대처하기가 어렵다.

<br/>

## Access Token & Refresh Token 활용법

**JWT 토큰 하나(Access Token)만을 사용하는 인증 방식은 탈취되었을 경우에 취약하다.** 서버에 토큰 정보를 저장하지 않고 토큰 자체로 인증하기 때문에 토큰을 가지고 있는 사람 모두가 권한을 가질 수 있다.

따라서 Access Token에 만료 기간을 두어 탈취에 대비해야하는데, 만료 기간을 짧게 설정하면 보안적인 측면에서는 좋지만, 사용자가 자주 로그인해야한다는 UX적 단점이 있다.

이를 보완하는 방법이 **추가적인 JWT 토큰(Refresh Token)을 사용하는 방법**이다. Access Token보다 더 긴 만료 기간을 가지고있는 Refresh Token을 추가로 두어 Access Token이 만료되었을 때 토큰을 재발급 받기 위한 인증 수단으로 사용하는 것이다.

![Access Token + Refresh Token](https://camo.githubusercontent.com/32bdb18e5014d84369fc5316b03000ae9428a79c8d857beb4cf4f2931fa0bd9f/68747470733a2f2f7374617469632e7061636b742d63646e2e636f6d2f70726f64756374732f393738313738343339353430372f67726170686963732f4230333635335f30385f30322e6a7067)

<br/>

## Reference

📄https://jwt.io/introduction  
📄http://bcho.tistory.com/999
📄https://mangkyu.tistory.com/56
📄https://etloveguitar.tistory.com/101
📄https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC
