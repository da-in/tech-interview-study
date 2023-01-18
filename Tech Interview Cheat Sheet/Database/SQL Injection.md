# SQL Injection

## SQL 인젝션이란?
SQL인젝션은 웹 사이트의 보안상 허점을 이용해 특정 SQL 쿼리 문을 전송하여 공격자가 원하는 DB의 중요한 정보를 가져오는 해킹기법이다.  
대부분 클라이언트가 입력한 데이터를 제대로 필터링하지 못하는 경우에 발생한다. 공격 난이도가 쉽고 피해 규모가 상당하기 때문에 보안 위협 1순위로 불릴 만큼 중요한 기법이다.

## SQL 인젝션 예시
[사진]

- 각 클라이언트가 자격증 번호를 조회할 수 있는 시스템.
- SQL 진행은 anjinma 클라이언트가 '자격증 번호 조회'를 클릭하여 anjinma 라는 이름이 웹서버에 전송되고 DB에 입력한 값과 일치하면 자격증 DB를 출력해준다.
- blackhat 클라이언트는 anjinma 클라이언트의 자격증 번호를 조회하기 위해서 SQL문을 수정하지만 권한이 없어서 자격증 정보를 가져올 수 없다.
- http://license12345.com/mysearch?=anjinma url을 전송할때 anjinma가 로그인 되어있으면 정상적으로 자격증 번호를 조회할 수 있지만 blackhat이 로그인 되어있으면 자격증 번호를 조회할 수 없다.
- 공격자인 blackhat은 url뒤에 ' or '1'='1'을 넣어줘서 항상 참이 되게 만들어서 자격증 번호를 조회해 온다.

## SQL 인젝션의 종류

1. **Error based SQL Injection - 논리적 에러를 이용한 SQL Injection**  
    - 앞서 예를 들어 설명한 기법으로 해당 기법으로 SQL 인젝션에 대한 기본을 설명하는게 일반적이다.
2. **UNION based SQL Injection = UNION 명령어를 이용한 SQL Injection** 
    - SQL UNION이란? 여러개의 SQL문을 합쳐 하나의 SQL문으로 만들어주는 방법이다.  
    - UNION과 UNION ALL로 나뉘는데 중복 값을 제외하고 안하고의 차이이다.  
        *select name from classa*   
        *union*   
        *select name from classb;*   
        하게 되면 클래스 A와 클래스 B 이름들이 합쳐져서 출력된다.   
        UNION으로 합쳐지는 두 테이블은 컬럼 갯수가 일치해야만 오류가 나지 않는다.  
    - [외부 입력]  
        ID: test' UNION SELECT 1,1 --  
        PW: anything
    - [실행 쿼리]  
        select * from users where id='test' UNION select 1,1 -- and PW='anything'
    - 쿼리가 실행되면 users 테이블에 등록된 id와 pw 목록을 전부 조회할 수 있게 된다.
3. **Blind SQL Injection - Boolean based Blind SQL Injection**  
    - Blind SQL Injection은 데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고, 단순히 참과 거짓의 정보만 알 수 있을 때 사용한다. 
    - 로그인 폼에 SQL Injection이 가능하다고 가정 했을 때, 서버가 응답하는 로그인 성공과 로그인 실패 메시지를 이용하여, DB의 테이블 정보 등을 추출해 낼 수 있다.

4. **Blind SQL Injection - Time based SQL**
    - Time Based SQL Injection 도 마찬가지로 서버로부터 특정한 응답 대신에 참 혹은 거짓의 응답을 통해서 데이터베이스의 정보를 유추하는 기법이다. 
    - 사용되는 함수는 MySQL 기준으로 SLEEP 과 BENCHMARK이다.


## SQL 인젝션 대응
1. **입력 값에 대한 검증**  
    SQL Injection 에서 사용되는 기법과 키워드는 엄청나게 많다. 사용자의 입력 값에 대한 검증이 필요한데, 서버 단에서 화이트리스트 기반으로 검증해야 한다. 블랙리스트 기반으로 검증하게 되면 수많은 차단리스트를 등록해야 하고, 하나라도 빠지면 공격에 성공하게 되기 때문이다.   
    공백으로 치환하는 방법도 많이 쓰이는데, 사실 이 방법도 취약한 방법이다. 예를 들어 공격자가 SESELECTLECT 라고 입력 시 중간의 SELECT가 공백으로 치환이 되면 SELECT 라는 키워드가 완성되게 된다. 따라서 공백 대신 공격 키워드와는 의미 없는 단어로 치환되어야 한다.
2. **Prepared Statement 구문사용**  
    요즘에 쓰이는 거의 모든 데이터베이스 엔진은 유저 입력이 의도치 않은 동작을 하는 걸 방지하는 escape 함수와 prepared statement를 제공한다. prepared statement 는 변수를 문자열로 바꾸는것이라 안전하다.  
    Prepared Statement 구문을 사용하게 되면, 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전에DBMS가 미리 컴파일 하여 실행하지 않고 대기합니다. 그 후 사용자의 입력 값을 문자열로 인식하게 하여 공격쿼리가 들어간다고 하더라도, 사용자의 입력은 이미 의미 없는 단순 문자열 이기 때문에 전체 쿼리문도 공격자의 의도대로 작동하지 않습니다.
3. **Error Message 노출 금지**  
    공격자가 SQL Injection을 수행하기 위해서는 데이터베이스의 정보(테이블명, 컬럼명 등)가 필요하다. 데이터베이스 에러 발생 시 따로 처리를 해주지 않았다면, 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환해 준다. 여기서 테이블명 및 컬럼명 그리고 쿼리문이 노출이 될 수 있기 때문에, 데이터베이스에 대한 오류발생 시 사용자에게 보여줄 수 있는 페이지를 제작 혹은 메시지박스를 띄우도록 해야한다.
4. **웹 방화벽 사용**  
    웹 공격 방어에 특화되어있는 웹 방화벽을 사용하는 것도 하나의 방법이다.  
    웹 방화벽은 소프트웨어 형, 하드웨어 형, 프록시 형 이렇게 세가지 종류로 나눌 수 있는데,   
    **소프트웨어 형** 은 서버 내에 직접 설치하는 방법이고,  
    **하드웨어 형** 은 네트워크 상에서 서버 앞 단에 직접 하드웨어 장비로 구성하는 것이며  
    **프록시 형** 은 DNS 서버 주소를 웹 방화벽으로 바꾸고 서버로 가는 트래픽이 웹 방화벽을 먼저 거치도록 하는 방법이다.

## 출처
https://m.blog.naver.com/lstarrlodyl/221837243294  
https://namu.wiki/w/SQL%20injection  
https://noirstar.tistory.com/264  