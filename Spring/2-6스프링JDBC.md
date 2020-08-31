JDBC는 java에서 DB연동에 쓰는 API
JDBC를 이용해서 DAO클래스를 쉽게 구현해서 디비연동을 쉽게 하자는 것

### JAVA의 순수 JDBC
JDBC : JDBC API를 이용하여 java로 DB연동  
JDBC Util : 커넥션 연결, 해제 로직 대체 가능  
but 여전히 중복 부분 많음  

### 스프링의 JDBC
Jdbc Template 클래스 : 템플릿 메소드 패턴 적용된 클래스

## 스프링 JDBC설정
1. dependency설정
2. Datasource설정
Datasource란?  
순수 jdbc로 데이터베이스에 접근을 하면, 데이터베이스에 접근할 때마다 connection을 맺고 끊는 작업을 한다.   
이 connection을 맺고 끊는 작업을 줄이기 위해 미리 connection을 생성해 두고, 데이터베이스에 접근하고자 하는 사용자에게 미리 생성된 connection을 제공하고 돌려받는다.  
이 connection들을 모아두는 장소를 connection pool이라 하며, Datasource는 java 에서 connection pool을 지원하기 위한 인터페이스이다.  
->디비 접근 connection을 미리 구현해놓은것!

### Jdbc Template 메소드
생략

## DAO클래스 구현
DAO클래스내에서 jdbc template 객체를 얻어서 구현해야 한다. 이 객체를 얻는 방법 2가지  
1. JdbDaoSupport클래스 상속  
2. JdbcTemplate클래스 <bean>등록, 의존성 주입  
