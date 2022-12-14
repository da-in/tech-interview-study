# HTTP Request Method

## HTTP Request Method

HTTP Request Method에는 아래와 같은 종류가 있다.

#### 1. GET

리소스를 검색하고, 반환받기 위해 사용되는 메소드이다.  
원하는 정보를 서버에 요청할 때 쓰인다.  
리소스의 위치를 URL에서 쿼리로 표현하기 때문에 RequestBody가 없다.

#### 2. HEAD

서버의 각종 정보를 확인하기 위해 사용되는 메소드이다.  
GET과 동일하지만, response에 Body가 없고 response Code와 Head만 응답받는다.

#### 3. POST

요청된 자원을 생성하기 위해 사용되는 메소드이다.  
POST로 정보를 전송하면 URL에 파라미터가 나타나지 않으므로 각종 데이터를 전송하는데 쓰인다.

#### 4. PUT

요청된 자원을 수정하기 위해 사용되는 메소드이다.  
전체 내용을 덮어쓰는 메소드이고, 없는 값을 수정할땐 새로 값을 생성함.

#### 5. PATCH

요청된 자원을 수정하기 위해 사용되는 메소드라는 점에서 PUT과 같지만, 해당 자원 전체를 수정하는 PUT과는 다르게 PATCH는 해당 자원의 일부 부분을 수정한다.

#### 6. DELETE

요청한 자원을 삭제하기 위해 사용되는 메소드이다.  
클라이언트에서 서버의 자원을 삭제할 수 있도록 허가하는 것은 매우 위험하다.  
서버 내 보안규칙이 존재하지 않으면 사용하기 위험하다.

#### 7. TRACE

루프백 메시지를 호출하기 위해 테스트용으로 사용되는 메소드이다.

#### 8. OPTION

웹서버에서 지원하는 메소드를 알기위해 사용되는 메소드이다.

#### 9. CONNECT

프록시 기능을 요청할 때 사용되는 메소드이다.

<br/>

## Get과 Post의 차이

대표적으로 쓰이는 것들은 GET, POST, PUT, PATCH, DELETE 이며 GET과 POST의 차이점은 다음과 같다.

#### GET

데이터를 조회하기 위해 사용되는 방식으로 데이터를 헤더에 추가하여 전송하는 방식이다.  
URL에 데이터가 노출되므로 보안적으로 중요한 데이터를 포함해서는 안된다.

#### POST

데이터를 추가 또는 수정하기 위해 사용되는 방식으로 데이터를 바디에 추가하여 전송하는 방식이다.  
완전히 안전하다는 것은 아니지만 URL에 데이터가 노출되지 않아 GET 보다는 안전하다.

---

## Reference

📄 https://gnaseel.tistory.com/24  
📄 https://dev-coco.tistory.com/161
