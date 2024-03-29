# 쿠키(Coockie)와 세션(Session)
HTTP 프로토콜의 특징이자 약점을 보완하기 위해 사용된다.

  1. Connectionless 프로토콜(비연결 지향)
  - 기본적으로 HTTP는 TCP 연결을 맺고 요청을 보내면 서버는 응답 한 후 연결이 끊어진다.(HTTP 1.1은 연결을 계속 유지하는 keep-alive 옵션이 존재한다)
  2. Stateless 프로토콜 (무상태)
  - 서버와의 연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 모든 상태 정보는 유지하지 않는 특성이 있다.
  
위와 같은 HTTP 프로토콜의 특징들은 서버와 클라이언트가 통신을 할 때 통신이 연속적으로 이어지지 않고 매번 통신을 재연결 해야한다.  
따라서 서버는 매 요청이 항상 처음인 상황이기 때문에 클라이언트가 누구인지 계속 인증을 해줘야 한다. 하지만 이러한 반복적인 작업은 매우 귀찮다.  
이것을 해결하기 위해 쿠키와 세션을 사용한다.

</br>

## 쿠키(Cookie)
사용자가 어떠한 웹 사이트를 방문할 경우, 그 사이트가 사용하고 있는 서버에서 사용자의 컴퓨터(클라이언트)에 저장하는 작은 기록 정보 파일이다.  
쿠키를 통해 HTTP에서 클라이언트의 상태 정보를 클라이언트의 PC에 저장하였다가 필요시 정보를 참조하거나 재사용할 수 있다.

- 쿠키 구성
  - 이름 : 쿠키를 구별하는 이름
  - 값 : 쿠키에 저장되는 값
  - 유효시간 : 쿠키 유지시간
  - 도메인 : 쿠키를 전송할 도메인
  - 경로 : 쿠키를 전송할 요청 경로

- 쿠키 특징  
  - 클라이언트에 총 300개의 쿠키를 저장할 수 있다.
  - 하나의 도메인 당 20개의 쿠키를 가질 수 있다.
  - 하나의 쿠키는 4KB(=4096byte)까지 저장 가능하다.
  - 제 3자도 쉽게 볼 수 있기 때문에 민감한 개인정보는 담지 않고, 간단한 정보들만 포함한다.
    
- 쿠키의 동작 순서
  - (1) 클라이언트가 페이지를 요청한다. (사용자가 웹사이트에 접근)
  - (2) 웹 서버는 쿠키를 생성한다.
  - (3) 생성한 쿠키에 정보를 담아 HTTP 응답을 돌려줄 때, 같이 클라이언트에게 돌려준다.
  - (4) 넘겨받은 쿠키는 클라이언트가 가지고 있다가(로컬 PC에 저장) 다시 서버에 요청할 때 쿠키도 같이 전송한다.
  - (5) 동일 사이트 재방문 시 클라이언트의 PC에 해당 쿠키가 있는 경우, 요청 페이지와 함께 쿠키를 전송한다.
  - (6) 서버는 같이 전송받은 쿠키를 확인함으로써 클라이언트를 식별할 수 있다.
    
- 사용 예시
  - 방문 사이트에서 로그인 시, "아이디와 비밀번호를 저장하시겠습니까?"
  - 팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크
  - 이후 다른 요청을 해도 쿠키를 통해 팝업 창이 뜨지 않는다.
</br>

## 세션(Session)
일정 시간 동안 같은 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술이다.  
여기서 일정 시간은 방문자가 웹 브라우저를 통해 웹 서버에 접속한 시점부터 웹 브라우저를 종료하여 연결을 끝내는 시점을 말한다.  
즉, 방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라고 한다. </br>
세션은 쿠키를 기반으로 하지만 쿠키와 다르게 서버 측에서 저장하고 관리한다.

- 세션 특징
  - 쿠키와 달리 웹 서버에 웹 컨테이너의 상태(세션)를 유지하기 위한 정보를 저장한다.
  - 웹 서버에는 보통 세션ID를 저장하고, 클라이언트에는 세션ID를 담은 쿠키가 저장된다.
  - 브라우저를 닫거나, 서버에서 세션을 삭제했을 때만 삭제가 되므로, 쿠키보다 비교적 보안이 좋다.
  - 저장 데이터에 제한이 없다. (서버 용량이 허용하는 한에서)
  - 각 클라이언트에 고유 세션ID를 부여한다. 세션ID로 클라이언트를 식별해 각 요청에 맞는 응답을 제공
    
- 세션의 동작 순서
  - 클라이언트가 페이지에 요청한다. (사용자가 웹사이트에 접근)
  - 서버는 접근한 클라이언트의 Request-Header의 필드인 Cookie를 확인하여, 클라이언트가 해당 session-id를 보냈는지 확인한다.
  - session-id가 존재하지 않는다면, 서버는 session-id를 생성해 클라이언트의 쿠키에 담아 돌려준다.
  - 서버에서 클라이언트로 돌려준 session-id를 쿠키를 사용해 서버에 저장한다.
  - 클라이언트는 재접속 시, session-id 값이 담긴 쿠키를 서버에 전달한다.
  - 서버는 해당 session-id 값을 확인하여 클라이언트를 식별하여 요청을 처리한다.
    
- 사용 예시
  - 화면을 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지

</br>

## 쿠키와 세션의 차이
||쿠키|세션|
|:------:|:------:|:------:|
|저장 위치|클라이언트(접속자PC)|웹 서버|
|저장 형식|text|Object|
|만료 시점|쿠키 저장시 설정(브라우저가 종료되어도, 만료시점까지 삭제되지 않음)|브라우저 종료시 삭제(기간 지정 가능)|
|사용하는 자원|클라이언트 리소스|웹 서버 리소스|
|용량 제한|총 300개, 하나의 도메인 당 20개, 하나의 쿠키 당 4KB|서버가 허용하는 한 용량제한 없음|
|속도|세션보다 빠름|쿠키보다 느림|
|보안|세션보다 안좋음|쿠키보다 좋음|

</br>

- 쿠키와 세션은 비슷한 역할을 하며, 동작 원리도 비슷하다. 그 이유는 세션도 결국 쿠키를 사용하기 때문이다.
- 큰 차이점은 사용자의 정보가 저장되는 위치이다. 쿠키는 서버의 자원을 전혀 사용하지 않으며, 세션은 서버의 자원을 사용한다.
- 보안 면에서 세션이 더 우수하다.
- 쿠키는 클라이언트 로컬에 저장되기 때문에 변질되거나 요청에서 스니핑을 당할 수 있어서 보안에 취약하지만,
- 세션은 쿠키를 이용해서 session-id만 저장하고 그것으로 구분하여 서버에서 처리하기 때문에 비교적 보안성이 높다.
- 라이프 사이클은 쿠키도 만료기간이 있지만 파일로 저장되기 때문에 브라우저를 종료해도 정보가 유지될 수 있다. 또한 만료기간을 따로 지정해 쿠키를 삭제할 때까지 유지할 수도 있다.
- 세션도 만료기간을 정할 수 있지만, 브라우저가 종료되면 만료기간에 상관없이 삭제된다.
- 쿠키는 쿠키 자체에 정보가 있기 때문에 서버에 요청 시 속도가 빠르고, 세션은 정보가 서버에 있기 때문에 처리가 요구되어 비교적 느린 속도를 낸다.

**중요 차이점 : 저장위치, 보안, 라이프사이클**

</br>

-----
## 출처
https://pearlluck.tistory.com/14  
https://hahahoho5915.tistory.com/32  
https://interconnection.tistory.com/74  
https://dev-coco.tistory.com/61</br>
https://code-lab1.tistory.com/298
