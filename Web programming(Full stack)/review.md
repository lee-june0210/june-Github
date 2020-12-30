> 201216_1일차

​

http / https 차이점 

https는 서버와 클라이언트 사이에 주고받는 정보를 암호화하여 처리

​
-----------------------------------------
> 201223_2일차

​

1. 우리가 흔히 브라우저 탐색을 할 때 스크롤을 하거나, 어떤 것을 클릭하면서 화면의 위치를 바꿀 때, 브라우저는 어떻게 다시 화면을 그릴까요?

2. 위에서 표현된 그림처럼 다시 렌더링 되지 않을까요? 

​

1-1. Render Tree는 HTML의 변환된 파일인 DOM Tree와 CSS의 변환된 파일인 CSS Tree 파일을 합친 결과물입니다. 이는 우리가 보는 Web Page를 구성하는 구성요소이다. 즉, 브라우저를 통해서 Web Page에서 스크롤이나 탐색을 할 때 브라우저는 Web Page 구성요소인 Render Tree를 저장하고 있다가, 정보만 가져와서 Paint만 하면 된다.

2-1. 따라서 다시 렌더링되지 않는다.

​
HTML을 해석해서 DOM Tree를 만들고, CSS를 해석해서 역시 CSS Tree(CSS Object Model)을 만듭니다. 

이 과정에서 Parsing 과정이 필요하며 토큰 단위로 해석되는 방식은 일반적인 소스코드의 컴파일 과정이라고 보시면 됩니다.

DOM Tree와 CSS Tree, 이 두 개는 연관되어 있으므로 Render Tree로 다시 조합됩니다.

이렇게 조합된 결과는 화면에 어떻게 배치할지 크기와 위치 정보를 담고 있습니다.

이후에 이렇게 구성된 Render Tree정보를 통해서 화면에 어떤 부분에 어떻게 색칠을 할지 Painting과정을 거치게 됩니다.

​

HTML 문서 안에 HTML태그뿐 아니라 CSS, JavaScript코드가 존재합니다.

JavaScript 코드는 body 태그 닫히기 전에 위치하는 것이 렌더링을 방해하지 않아도 좋고, css코드는 head 안에 위치해서 렌더링 처리 시에 브라우저가 더 빨리 참고할 수 있게 하는 것이 좋습니다.

​

​

웹서버

웹 서버의 가장 중요한 기능은 클라이언트(Client)가 요청하는 HTML 문서나 각종 리소스(Resource)를 전달하는 것입니다.

​

HTML 태그

    <nav> 네이게이션 영역

    <ul>이란 unlisted? 순서가 상관없는 리스트


---------------------------------------

> 201229 3일차

JDK, Eclipse, apache Tomcat 설치 및 환경 설정 완료

--------------------------------
> 201230 4일차 

##### 5-1 서블릿이란?

자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할입니다.

서블릿을 정의해보면 서블릿(servlet)은 WAS에 동작하는 JAVA 클래스입니다. 

서블릿은 HttpServlet 클래스를 상속받아야 합니다.

서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두 가지(JSP, 서블릿)를 조화롭게 사용해야 합니다.

예를 들어, 웹 페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현합니다.

##### 5-2 Servlet 작성법

tlqkf 날라갔어..........

서블릿 2.5에서는 web.xml 선택?을 필수적으로 해줘야한다. 서블릿 3.1에서는 

###### 5-3 Servlet 라이프 싸이클
service(request, response) 메소드

HttpServlet의 service메소드는 템플릿 메소드 패턴으로 구현합니다.

클라이언트의 요청이 GET일 경우에는 자신이 가지고 있는 doGet(request, response)메소드를 호출
클라이언트의 요청이 Post일 경우에는 자신이 가지고 있는 doPost(request, response)를 호출
 
LifecycleServlet 수정 실습

Service(request, response)메소드 주석처리
HttpServlet의 doGet(request, response)메소드 오버라이딩
HttpServlet의 doPost(request, response)메소드 오버라이딩