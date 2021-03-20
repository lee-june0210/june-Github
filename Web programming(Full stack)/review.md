## 세번째 프로젝트 시작_210215

프레임 워크 모듈

스프링 프레임워크는 약 20개의 모듈로 구성되어 있습니다.
필요한 모듈만 가져다 사용할 수 있습니다.

### Spring Framework란?

엔터프라이즈급 어플리케이션을 구축할 수 있는 가벼운 솔루션이자, 원스-스탑-숍(One-Stop-Shop)
원하는 부분만 가져다 사용할 수 있도록 모듈화가 잘 되어 있습니다.
IoC 컨테이너입니다.
선언적으로 트랜잭션을 관리할 수 있습니다.
완전한 기능을 갖춘 MVC Framework를 제공합니다.
AOP 지원합니다.
스프링은 도메인 논리 코드와 쉽게 분리될 수 있는 구조로 되어 있습니다.

<img src ="https://user-images.githubusercontent.com/76678910/107940752-1322ee80-6fcc-11eb-8a58-cd0d11ba7b3a.png" > </img>

* AOP 와 인스트루멘테이션 (Instrumentation)

spring-AOP : AOP 얼라이언스(Alliance)와 호환되는 방법으로 AOP를 지원합니다.
spring-aspects : AspectJ와의 통합을 제공합니다.
spring-instrument : 인스트루멘테이션을 지원하는 클래스와 특정 WAS에서 사용하는 클래스로 더 구현체를 제공합니다. 참고로 BCI(Byte Code Instrumentations)은 런타임이나 로드(Load) 때 클래스의 바이트 코드에 변경을 가하는 방법을 말합니다.
 

* 메시징(Messaging)

spring-messaging : 스프링 프레임워크 4는 메시지 기반 어플리케이션을 작성할 수 있는 Message, MessageChannel, MessageHandler 등을 제공합니다. 또한, 해당 모듈에는 메소드에 메시지를 맵핑하기 위한 어노테이션도 포함되어 있으며, Spring MVC 어노테이션과 유사합니다.
 

데이터 엑서스(Data Access) / 통합(Integration)

데이터 엑세스/통합 계층은 JDBC, ORM, OXM, JMS 및 트랜잭션 모듈로 구성되어 있다.
spring-jdbc : 자바 JDBC프로그래밍을 쉽게 할 수 있도록 기능을 제공합니다.
spring-tx : 선언적 트랜잭션 관리를 할 수 있는 기능을 제공합니다.
spring-orm : JPA, JDO및 Hibernate를 포함한 ORM API를 위한 통합 레이어를 제공합니다.
spring-oxm : JAXB, Castor, XMLBeans, JiBX 및 XStream과 같은 Object/XML 맵핑을 지원합니다.
spring-jms : 메시지 생성(producing) 및 사용(consuming)을 위한 기능을 제공, Spring Framework 4.1부터 spring-messaging모듈과의 통합을 제공합니다.
 

웹(Web)

웹 계층은 spring-web, spring-webmvc, spring-websocket, spring-webmvc-portlet 모듈로 구성됩니다.
spring-web : 멀티 파트 파일 업로드, 서블릿 리스너 등 웹 지향 통합 기능을 제공한다. HTTP클라이언트와 Spring의 원격 지원을 위한 웹 관련 부분을 제공합니다.
spring-webmvc : Web-Servlet 모듈이라고도 불리며, Spring MVC 및 REST 웹 서비스 구현을 포함합니다.
spring-websocket : 웹 소켓을 지원합니다.
spring-webmvc-portlet : 포틀릿 환경에서 사용할 MVC 구현을 제공합니다.

컨테이너(Container)

컨테이너는 인스턴스의 생명주기를 관리하며, 생성된 인스턴스에게 추가적인 기능을 제공합니다.

예를 들어, Servlet을 실행해주는 WAS는 Servlet 컨테이너를 가지고 있다고 말합니다.

WAS는 웹 브라우저로부터 서블릿 URL에 해당하는 요청을 받으면, 서블릿을 메모리에 올린 후 실행합니다.
개발자가 서블릿 클래스를 작성했지만, 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet 컨테이너입니다.

Servlet컨테이너는 동일한 서블릿에 해당하는 요청을 받으면, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행하여 그 결과를 웹 브라우저에게 전달합니다.

컨테이너는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하는 것을 말합니다.



IoC(Inversion of Control) 

컨테이너가 코드 대신 오브젝트의 제어권을 갖고 있어 IoC(제어의 역전)이라 합니다.
예를 들어, 서블릿 클래스는 개발자가 만들지만, 그 서블릿의 메소드를 알맞게 호출하는 것은 WAS입니다.
이렇게 개발자가 만든 어떤 클래스나 메소드를 다른 프로그램이 대신 실행해주는 것을 제어의 역전이라고 합니다.

 

DI(Dependency Injection)

DI는 의존성 주입이란 뜻을 가지고 있으며, 클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말합니다.

## 두번째 프로젝트 시작_210113

jsp는 자체적으로 동작되는게 아니라 모두 서블릿으로 바뀌어 동작한다. 서블릿으로 바뀐 후에는 서블릿의 라이프 싸이클과 똑같은 형식으로 작동한다

#### 스크립스 요소

<img src = "https://user-images.githubusercontent.com/76678910/107172903-dd996680-6a09-11eb-874c-9b043fbe4f0f.png" height = "70%" width = "70%"> </img>

* <%@ %>는 페이지 지시자라고 하는데 서블릿으로 바뀔때 동작 하는 방법을 알려준다.
* <%= %>는 표현식이라고 한다. (= out.print(total))
* <%! %> 선언식이다. 클래스에서 변수나 메서드를 선언한다거나 필드를 선언할때 넣어준다. 매서드 뿐만아니라 특정 매서드를 서비스 매서드가 아니라, 필드나 매서드로 내가 지정하고 싶다면 선언식을 사용하면 도니다.

#### 주석

1. HTML 주석

HTML 주석은 <!--로 시작해서 -->로 끝나는 형태
HTML 주석은 HTML주석을 사용한 페이지를 웹에서 서비스할 때 화면에 주석이 내용이 표시되지는 않으나 , [소스보기]수행하면 HTML주석의 내용이 화면에 표시.
HTML주석의 예시
```
<!-- html 주석입니다. -->
```
2. JSP주석

JSP 페이지에서만 사용되며 <%--로 시작해서 --%>로 끝나는 형태
JSP 주석은 해당 페이지를, 웹 브라우저를 통해 출력 결과로서 표시하거나, 웹 브라우저 상에서 소스 보기를 해도 표시 되지 않음. 또한 JSP주석 내에 실행코드를 넣어도 그 코드는 실행되지 않음.
JSP주석의 예시
```
<%-- JSP 주석입니다. --%>
```
3. 자바주석

자바 주석은 //, /**/을 사용해서 작성.
//은 한 줄짜리 주석을 작성할 때 사용되고, /**/은 여러 줄의 주석을 작성할 때 사용
스크립트릿이나 선언문에서 사용되는 주석으로, 자바와 주석 처리 방법이 같음
자바주석의 예시
```
//주석
/*주석
여러 줄에 걸친 주석이다.
*/
```

HTMl <!-- --> 
JSP <%-- --> 
Java // or /* */ 

"각각 경우에 따라서 주석이 하는 역할 >> 주석이 주석일 때에  위치가 다를 수 있다."를 기억.

#### JSP의 내장객체

<img src ="https://user-images.githubusercontent.com/76678910/106701837-ace0b800-662a-11eb-9d98-e7d5ea027d29.png" ></img>

JavaScript의 기본문법을 이해한다.
DOM, Browser Event, Ajax이 각각 무엇인지 이해하고, 이를 활용해 웹화면을 제어할 수 있다.
JSP의 라이프사이클을 이해하고 redirect & forward 와 scope를 이해하고 사용할 수 있다. 
JSTL과 EL을 사용할 수 있다. 
데이터베이스를 설치하고 간단한 SQL을 사용할 수 있다. 
Maven을 이해하고 Maven을 이용한 웹 어플리케이션을 작성할 수 있다. 
JDBC 프로그래밍을 할 수 있다. 
Web API를 이해한다. 

> 210208
#### SCOPE


<img src = "https://user-images.githubusercontent.com/76678910/107175267-bcd40f80-6a0f-11eb-813f-0a5a4583c5cd.jpg" height = "40%" width = "40%"> </img>


* Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
Application.setAttribute() Application.getAttribute()
* Session : 웹 브라우저 별로 변수가 관리되는 경우 사용
Session.setAttribute() Session.getAttribute()
ex) 로그인, 장바구니 정보
* Request : http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용
Request.setAttribute() Request.getAttribute()
포워딩이나 리다이렉트를 하더라도 없어지지 
http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우 사용한다.
HttpServletRequest 객체를 사용한다.
JSP에서는 request 내장 변수를 사용한다.
서블릿에서는 HttpServletRequest 객체를 사용한다.
값을 저장할 때는 request 객체의 setAttribute()메소드를 사용한다.
값을 읽어 들일 때는 request 객체의 getAttribute()메소드를 사용한다.
forward 시 값을 유지하고자 사용한다.
앞에서 forward에 대하여 배울 때 forward 하기 전에 request 객체의 setAttribute() 메소드로 값을 설정한 후, 서블릿이나 jsp에게 결과를 전달하여 값을 출력하도록 하였는데 이렇게 포워드 되는 동안 값이 유지되는 것이 Request scope를 이용했다고 합니다.
* Page : 페이지 내에서 지역변수처럼 사용
포워드를 할때 pageContext는 없어진다 
PageContext.setAttribute() PageContext.getAttribute()
like 지역변수
서블릿에서는 거의 사용안함


>210208
와............진심 진짜................Server Tomcat v8.0 Server at localhost failed to start. 이 오류만 진짜 1시간 반뜬 것같다. 하란거 다해봤는데.........쟤때매 ㄹㅇ 공기까지 답답해지고 두통 오지게 왔음.........................................................자주 봐서 그만큼 익숙해졌다 싶었는데 오늘 역대급으로 해결안됐음.......................

1. windows -> preferences 가서 JAVA BUILD PATH가서 jdk랑 톰캣 지우고 다시 설치
2. 빨강불인 애들 각각 프로젝트 preferences가서 JAVA BUILD PATH 지우고 다시 설치
3. 그래도 안되면 .m2 폴더 삭제하고 update project 한다음에 다시 1번부터 해보기

>210209
이유 없는 빨간 엑스
-> 다이나믹 웹 머시기 버전 문제일 가능성있음
navigator가서 ~~~core.xml 누르고 java랑 다이나믹 웹 머시기 각각 1.8(jdk버전 맞춘거임) 3.1로 설치한다음 
Maven 프로젝트 업데이트 해주고
다시 해당 프로젝트 proference?가서 Build Path랑 Facet 재설정 해주면 엑박없어짐

>210114
* Maven이란?

Maven은 지금까지 애플리케이션을 개발하기 위해 반복적으로 진행해왔던 작업들을 지원하기 위하여 등장한 도구입니다. 
Maven을 사용하면 빌드(Build), 패키징, 문서화, 테스트와 테스트 리포팅, git, 의존성관리, svn등과 같은 형상관리서버와 연동(SCMs), 배포 등의 작업을 손쉽게 할 수 있습니다.
Maven을 이해하려면 CoC(Convention over Configuration)라는 단어를 먼저 이해해야 합니다.
CoC란 일종의 관습을 말하는데, 예를 들자면 프로그램의 소스파일은 어떤 위치에 있어야 하고, 소스가 컴파일된 파일들은 어떤 위치에 있어야 하고 등을 미리 정해놨다는 것입니다.
이 말은 관습에 이미 익숙한 사용자는 쉽게 Maven을 사용할 수 있는데, 관습에 익숙하지 않은 사용자는 이러한 제약사항에 대해서 심한 거부감을 느낄 수 있습니다.
Maven을 사용한다는 것은 어쩌면 이러한 관습 즉 CoC에 대해서 알아나가는 것이라고도 말할 수 있습니다. 


* 장점

Maven을 사용할 경우, 굉장히 편리한 점들이 많습니다.
많은 사람이 손꼽는 장점 중에는 편리한 의존성 라이브러리 관리가 있습니다.
앞에서 JSTL을 학습할 때, 몇 가지 파일을 다운로드 하여 /WEB-INF/lib폴더에 복사하여 사용했었습니다.
관련된 라이브러리가 많아질수록 이러한 방식은 상당히 불편해집니다.
Maven을 사용하면 설정 파일에 몇 줄 적어줌으로써 직접 다운로드 받거나 하는 것을 하지 않아도 라이브러리를 사용할 수 있습니다.
프로젝트에 참여하는 개발자가 많아지게 되면, 프로젝트를 빌드하는 방법에 대하여 가이드하는 것도 쉬운 일이 아닙니다.
Maven을 사용하게 되면 Maven에 설정한 대로 모든 개발자가 일관된 방식으로 빌드를 수행할 수 있게 됩니다.
Maven은 또한 다양한 플러그인을 제공해줘서, 굉장히 많은 일들을 자동화시킬 수 있습니다.

> 210115

Maven으로 생성된 프로젝트의 경우 자바 소스는 src/main/java 폴더에 생성됩니다.
웹 어플리케이션과 관련된 html, css등은 src/main/webapp 폴더에서 작성해야 합니다.

> 210118

프로그램 로직 수행은 Servlet에서, 결과 출력은 JSP에서 하는 것이 유리하다.
JSP에서는 되도록 자바 코드를 줄이는 것이 좋아요. 이를 위해서 제공되는 문법이 JSTL과 EL이에요.

### redirect vs forward

redirect는요. 클라이언트가 서버한테 요청을 보냈고요.그러면 이 서버는 어떤 일들을 처리하고 다시 어떻게 하냐면클라이언트한테 새로운 요청할 곳을 알려주면서 이걸로 다시 요청해요. 라고 주는 것이 리다이렉트에요.그래서 리다이렉트의 결과는 실제 실행한 다음에 url 주소가 바뀌었었던 거 혹시 기억하실까요? 그런데 포워드는요. 클라이언트는 요청을 보냈어요. 그런데 서버쪽에서 그 요청에 대해서 혼자 처리하는 것이 아니라 다른 누군가. back한테 처리를 맡기는 거죠. 이런 것을 포워드라고 하는데 이때 클라이언트는 이 서블릿, 요청받은 Servlet 1이 혼자서 다 처리해서 응답을 했는지 아니면 다른 누군가한테 부탁해서 처리를 했는지.
여기까지는 전혀 알 필요가 없어요.
그래서 포워드가 실행된 다음에는 url이 바뀌지 않아요. 

실제 클라이언ㅌ가 서버한테 요청을 하면 반드시 request와 response가 존재했다. was는 요청을 담당하고 있는 responces객체를 만드어서 요청이 들어와서 완료될때까지 계속 
forward는 저 객체가 1번 만들어지는 건데 redirect는 여러번 요청이 들어가서 각각 request와 response가 만들어진다.

### 리다이렉트

* 리다이렉트는 HTTP프로토콜로 정해진 규칙이다.
* 서버는 클라이언트의 요청에 대해 특정 URL로 이동을 요청할 수 있다. 이를 리다이렉트라고 한다.
* 서버는 클라이언트에게 HTTP 상태코드 302로 응답하는데 이때 헤더 내 Location 값에 이동할 URL 을 추가한다. 클라이언트는 리다이렉션 응답을 받게 되면 헤더(Location)에 포함된 URL로 재요청을 보내게 된다. 이때 브라우저의 주소창은 새 URL로 바뀌게 된다..
* 클라이언트는 서버로부터 받은 상태 값이 302이면 Location헤더값으로 재요청을 보내게 된다. 이때 브라우저의 주소창은 전송받은 URL로 바뀌게 된다.
* 서블릿이나 JSP는 리다이렉트하기 위해 HttpServletResponse 클래스의 sendRedirect() 메소드를 사용한다.

리다이렉션을 하는 이유
HTTP 애플리케이션은 언제나 아래 세가지를 원하기 때문에 리다이렉션은 현대의 웹에서는 불가피합니다.

신뢰할 수 있는 HTTP 트랜잭션의 수행
지연 최소화
네트워크 대역폭 절약

위와 같은 이유들 때문에, 웹 콘텐츠는 흔히 여러장소에 배포하게 됩니다.
이렇게 하면 한곳에서 실패한 경우 다른 곳을 이용할 수 있으므로 신뢰성 이 개선됩니다.
또한 클라이언트가 보다 가까운 리소스에 접근할 수 있게 되어 응답시간도 줄여줍니다.
또한 목적지 서버가 분산되므로 네트워크 혼잡도도 줄어들게 됩니다.
이렇게 리다이렉션이란 최적의 분산된 콘텐츠를 찾는 것을 도와주는 기법의 집합이라고 할 수 있습니다.

리다이렉션 구현에는 load-balancing(부하 균형)의 과제가 포함되는데, 왜냐하면 둘은 서로 공존하기 떄문입니다.(대부분의 리다이렉션 장치들은 몇가지 방식의 부하 균형을 포함)

리다이렉션이 필요한 곳
도메인 앨리어싱

1. 링크 유지하기
2. 안전하지 않은 요청에 대한 일시적인 응답
3. 긴 요청에 대한 일시적인 응답

### forward란?

웹 브라우저에서 Servlet1에게 요청을 보냄
Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송

<img src = "https://user-images.githubusercontent.com/76678910/106856801-68c0e680-6702-11eb-9a6c-864fd8a5a6e6.png" height = "40%" width = "40%"> </img>

```java
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            
            int diceValue = (int)(Math.random() * 6) + 1; 
            request.setAttribute("dice", diceValue);
            // 맡겨 놓을 수 있는 객체를 setAttribute라고 한다. diceValue는 세탁물이고
	    //"dice"는 맡긴 이름. 나중에 "dice"라고 찾으면 diceValue값이 나온다. 

            RequestDispatcher requestDispatehcer = request.getRequestDispatcher("/next"); // 포워드하는 코드
            requestDispatehcer.forward(request, response); // 얘도 포워드 하기 위해 무조건 적어야하나봐
```


```java
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>form</title></head>");
        out.println("<body>");

        int dice = (Integer)request.getAttribute("dice");
        out.println("dice : " + dice);
        for(int i = 0; i < dice; i++) {
            out.print("<br>hello");
        }
        out.println("</body>");
        out.println("</html>");
    }
```

### JDBC란? 
* JDBC(Java Database Connectivity)의 정의
	- 자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약
	- 자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API
	- SQL과 프로그래밍 언어의 통합 접근 중 한 형태


<img src="https://user-images.githubusercontent.com/76678910/104908054-407a7d80-59c9-11eb-9c95-4339af860c07.png" width="60%" height="60%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>

보통은 이런 JDBC를 직접 사용하지 않고 프레임워크를 쓴다 하지만 이렇게 원리를 이해하고 사용하면 문제해결이 보다 용이해진다. 

#### IMPORT
```java
import java.sql.*;
``` 
#### 드라이버 로드
```java
Class.forName( "com.mysql.jdbc.Driver" );
``` 
#### Connection 얻기
```java
String dburl  = "jdbc:mysql://localhost/dbName";
Connection con =  DriverManager.getConnection ( dburl, ID, PWD );
```
#### 소스코드 예제
```java
public static Connection getConnection() throws Exception{
	String url = "jdbc:oracle:thin:@117.16.46.111:1521:xe";
	String user = "smu";
	String password = "smu";
	Connection conn = null;
	Class.forName("oracle.jdbc.driver.OracleDriver");
	conn = DriverManager.getConnection(url, user, password);
	return conn;
}
``` 
#### Statement 생성
```java
Statement stmt = con.createStatement();
```
#### 질의 수행
```java
ResultSet rs = stmt.executeQuery("select no from user" );
```
#### ResultSet으로 결과 받기
```java
ResultSet rs =  stmt.executeQuery( "select no from user" );
while ( rs.next() )
      System.out.println( rs.getInt( "no") );
```
#### Close
```java
rs.close();
stmt.close();
con.close();
```
>210201
1. jdbc 에러 3일을 안돼서 절망하고 있었는데 maven 플젝 만들면서 pom.xml에 jdbc 관련 코드를 추가를 안해서 그랬었다................................
그래 나머지는 잘했던거야....대견해...

2. 아 tododto3에서 개 안받아지더니 ㄹㅇ 백번 다시보니깐 tododao에서 받아오고 있었음;;; 그러니깐 안되지ㅎㅎ 역시 다~~~ 내잘못^^

### REST API
REST API란?

REST는 REpresentational State Transfer라는 용어의 약자
REST API란 말 그대로 REST형식의 API를 말합니다. 

REST API란 핵심 컨텐츠 및 기능을 외부 사이트에서 활용할 수 있도록 제공되는 인터페이스입니다.

예를 들어, 네이버에서 블로그에 글을 저장하거나, 글 목록을 읽어갈 수 있도록 외부에 기능을 제공하거나 우체국에서 우편번호를 조회할 수 있는 기능을 제거하거나, 구글에서 구글 지도를 사용할 수 있도록 제공하는 것들을 말합니다.
웹 브라우저 뿐만 아니라 앱 등 다양한 클라이언트가 등장하면서 그러한 클라이언트들에게 대응하기 위해 REST API가 널리 사용되기 시작하였습니다.

서비스 업체들이 다양한 REST API를 제공함으로써, 클라이언트는 이러한 REST API들을 조합한 어플리케이션을 만들 수 있게 되었습니다.

이를 매시업(Mashup)이라고 합니다.

### Web API
API는  Application Programming Interface의 약자입니다.
“API(Application Programming Interface, 응용 프로그램 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻합니다.

Web API 디자인 가이드

URI는 정보의 자원을 표현해야 합니다.
자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현합니다.


##  첫번째 프로젝트 시작_210101

> 210104 9일차 

#### 디버깅 성공?

이클립스, jdk, 톰캣 싹 다 다시 깔고 오류의 시작이었던 HeaderServlet 성공.ㅠㅠㅠㅠㅠ

#### 프로젝트 진행중
### HTML안에 이미지 넣기

1. HTML 파일 내에 이미지 파일이 있는 경우 : 이미지 이름 넣기

       <img src="이미지 경로" alt="이미지없을 때 나타나는 텍스트">

2. 다른 서버에 있는 이미지를 사용하는 경우

        <img src="이미지 경로" alt="이미지없을 때 나타는 텍스트">

3. 이미지URL을 링크하는 경우 : hyperlink tag 사용

        <a href="이미지가 있는 사이트의 주소">
         <img src="이미지의 주소" alt="이미지 없을 때 나타나는 텍스트">
        </a>



-------------------------------

>210103 8일차 

#### 디버깅

서블릿 생성하는 부분에서 오류가 처음 발생하고 더 번져서 해결 못함.....
톰캣 오류 수정하는 부분에서 이것저것 건들이다가 경로를 다 망쳐놓은듯...
시바......다 지우고 다시 깔아야하나..................................



--------------------------------
> 210101 7일차 

#### 오류 발생

서블릿 생성 부분에서 첫 오류 발생...이유 불명
일단 톰캣쪽 오류인듯.

--------------------------------
> 201231 6일차 

#### 3 CSS

float를 부모에게 자식으로 인식시키기 -> overflow

float 다른 엘리먼트에 인식시키기 -> clear


--------------------------------

> 201230_5일차 

#### 5-1 서블릿이란?

자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할입니다.

서블릿을 정의해보면 서블릿(servlet)은 WAS에 동작하는 JAVA 클래스입니다. 

서블릿은 HttpServlet 클래스를 상속받아야 합니다.

서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두 가지(JSP, 서블릿)를 조화롭게 사용해야 합니다.

예를 들어, 웹 페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현합니다.

#### 5-2 Servlet 작성법

tlqkf 날라갔어..........

서블릿 2.5에서는 web.xml 선택?을 필수적으로 해줘야한다. 서블릿 3.1에서는 어노테이션 작업이 자동으로 된다.////////.........?........

#### 5-3 Servlet 라이프 싸이클
service(request, response) 메소드

HttpServlet의 service메소드는 템플릿 메소드 패턴으로 구현합니다.

클라이언트의 요청이 GET일 경우에는 자신이 가지고 있는 doGet(request, response)메소드를 호출
클라이언트의 요청이 Post일 경우에는 자신이 가지고 있는 doPost(request, response)를 호출
 
LifecycleServlet 수정 실습

Service(request, response)메소드 주석처리
HttpServlet의 doGet(request, response)메소드 오버라이딩
HttpServlet의 doPost(request, response)메소드 오버라이딩

#### 1번 프로젝트 시작

 

1. position 속성으로 특별한 배치를 할 수 있습니다.

position 속성은 기본 static입니다.

그냥 순서대로 배치됩니다.

 

2. absolute는 기준점에 따라서 특별한 위치에 위치합니다.

top / left / right / bottom 으로 설정합니다.

기준점을 상위엘리먼트로 단계적으로 찾아가는데 static이 아닌 position이 기준점입니다.

 

3. relative는 원래 자신이 위치해야 할 곳을 기준으로 이동합니다.

top / left / right / bottom로 설정합니다.

 



엘리먼트가 배치되는 방식 (margin:10px)

margin으로 배치가 달라질 수 있습니다.

margin은 위 / 아래 / 좌 / 우 엘리먼트와 본인 간의 간격입니다.

따라서 그 간격만큼 내 위치가 달라집니다.


엘리먼트가 배치되는 방식 (float:left)

float 속성으로 원래 flow에서 벗어날 수 있고 둥둥 떠다닐 수 있습니다.

일반적인 배치에 따라서 배치된 상태에서 float는 벗어난 형태로 특별히 배치됩니다.

따라서 뒤에 block엘리먼트가 float 된 엘리먼트를 의식하지 못하고 중첩돼서 배치됩니다.




엘리먼트가 배치되는 방식 (box-model)

블록 엘리먼트의 경우 box의 크기와 간격에 관한 속성으로 배치를 추가 결정합니다.

margin, padding, border, outline으로 생성되는 것입니다.



box-shadow 속성도 box-model에 포함지어 설명할 수 있습니다.

box-shadow는 border 밖에 테두리를 그릴 수 있는 속성입니다.



box-sizing과 padding

padding 속성을 늘리면 엘리먼트의 크기가 달라질 수 있습니다.

box-sizing 속성으로 이를 컨트롤 할 수 있습니다.

box-sizing 속성을 border-box로 설정하면 엘리먼트의 크기를 고정하면서 padding 값만 늘릴 수 있습니다.


 

layout 구현방법은?

전체 레이아웃은 float를 잘 사용해서 2단, 3단 컬럼 배치를 구현합니다.

엘리먼트안의 텍스트의 간격과 다른 엘리먼트간의 간격은 padding과 margin 속성을 잘 활용해서 위치시킵니다.





-----------------------------------------



> 201229_4일차

JDK, Eclipse, apache Tomcat 설치 및 환경 설정 완료

---------------------------------------

> 201228_3일차

#### 2 HTML

HTML 태그

    <nav> 네이게이션 영역

    <ul>이란 unlisted? 순서가 상관없는 리스트




-----------------------------------------
> 201223_2일차


#### 생각해보기

1. 우리가 흔히 브라우저 탐색을 할 때 스크롤을 하거나, 어떤 것을 클릭하면서 화면의 위치를 바꿀 때, 브라우저는 어떻게 다시 화면을 그릴까요?

2. 위에서 표현된 그림처럼 다시 렌더링 되지 않을까요? 



1-1. Render Tree는 HTML의 변환된 파일인 DOM Tree와 CSS의 변환된 파일인 CSS Tree 파일을 합친 결과물입니다. 이는 우리가 보는 Web Page를 구성하는 구성요소이다. 즉, 브라우저를 통해서 Web Page에서 스크롤이나 탐색을 할 때 브라우저는 Web Page 구성요소인 Render Tree를 저장하고 있다가, 정보만 가져와서 Paint만 하면 된다.

2-1. 따라서 다시 렌더링되지 않는다.


HTML을 해석해서 DOM Tree를 만들고, CSS를 해석해서 역시 CSS Tree(CSS Object Model)을 만듭니다. 

이 과정에서 Parsing 과정이 필요하며 토큰 단위로 해석되는 방식은 일반적인 소스코드의 컴파일 과정이라고 보시면 됩니다.

DOM Tree와 CSS Tree, 이 두 개는 연관되어 있으므로 Render Tree로 다시 조합됩니다.

이렇게 조합된 결과는 화면에 어떻게 배치할지 크기와 위치 정보를 담고 있습니다.

이후에 이렇게 구성된 Render Tree정보를 통해서 화면에 어떤 부분에 어떻게 색칠을 할지 Painting과정을 거치게 됩니다.



HTML 문서 안에 HTML태그뿐 아니라 CSS, JavaScript코드가 존재합니다.

JavaScript 코드는 body 태그 닫히기 전에 위치하는 것이 렌더링을 방해하지 않아도 좋고, css코드는 head 안에 위치해서 렌더링 처리 시에 브라우저가 더 빨리 참고할 수 있게 하는 것이 좋습니다.




웹서버

웹 서버의 가장 중요한 기능은 클라이언트(Client)가 요청하는 HTML 문서나 각종 리소스(Resource)를 전달하는 것입니다.




> 201216_1일차


#### http / https 차이점 

https는 서버와 클라이언트 사이에 주고받는 정보를 암호화하여 처리

