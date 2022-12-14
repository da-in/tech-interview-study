# **Authentication(인증)과 Authorization(인가)**

## **Authentication(인증)이란?**

**Authentication**(인증)은 사용자의 신원을 확인하는 과정이야!
<br/>
로그인을 그 예시로 들 수 있는데, 우리는 로그인 과정에서 아이디와 비번이라는 증거를 제시하지!
<br/>
그 증거를 통해 사용자는 자신의 신원을 인정받을 수 있는거야.
이걸 **Authentication**(인증)이라 해.
<br/>
인증의 결과로 Authorization(인가)에 필요한 구별가능한 증거(인가 토큰)를 발급받을 수 있어!

## **Authorization(인가)란?**

**Authorization(인가)는 간단히 말하자면 유저에 대한 권한을 허락하는 과정이야.**
<br/>
즉, 사용자가 어떤 리소스에 접근할 수 있는지 또는 어떤 동작을 수행할 수 있는지 검증하는 것이지.

이해하기 쉽게 예를 들어볼게. 우리가 공연장에 입장하기 위해 티켓을 구매하는 상황이라 상상해보자.
<br/>
입장할 때 공연장은 우리의 신원이 무엇인지에 대해서는 관심이 없어.
그저 우리가 공연장에 입장할 권한이 있는지 여부에만 관심이 있을 뿐이지.
입장 권한을 증명하려면 우리는 신원여부와 상관없이 티켓만 있으면 되잖아?

위 예시처럼 사용자의 신원을 확인하는 **Authentication(인증)** 이 이루어지지 않았다 해도, **Authentication(인가)** 과정에서 검증이 실패한다는 것은 아니야!

Authentication(인가)를 위해서 Authentication(인증)을 통해 얻은 증거(인가 토큰)을 사용해.
<br/>
사용자가 어떠한 요청을 보낼 때 이 증거를 함께 첨부하여 보냄으로써 검증하고, 요청을 처리해.

## **정리**

|                             | Authentication(인증)                  | Authorization(인가)            |
| :-------------------------- | :------------------------------------ | :----------------------------- |
| 기능                        | 자격 증명 확인                        | 권한 허가/거부                 |
| 진행방식                    | 비밀번호, 생체인식, 일회용 핀 또는 앱 | 보안 팀에서 관리하는 설정 사용 |
| 사용자가 볼 수 있는가       | ⭕                                    | ❌                             |
| 사용자가 직접 변경 가능한가 | ⭕(부분적으로 가능)                   | ❌(불가능)                     |
| 데이터 전송                 | ID 토큰 사용                          | 액세스 토큰 사용               |

## 출처

https://www.okta.com/kr/identity-101/authentication-vs-authorization/
<br/>
https://velog.io/@aaronddy/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization
<br/>
https://dextto.tistory.com/234
<br/>
https://ivorycode.tistory.com/entry/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization
