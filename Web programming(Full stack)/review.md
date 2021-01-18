

## 두번째 프로젝트 시작_210113


jsp는 자체적으로 동작되는게 아니라 모두 서블릿으로 바뀌어 동작한다. <%%>는 지시자라고 하는데 서블릿으로 바뀔때 동작 하는 방법을 알려준다.
<%= %>는 표현식이라고 한다. (= out.print(total))
<%! %> 선언식이다. 클래스에서 메서드를 선언한다거나 필드를 선언할때 넣어준다. 매서드 뿐만아니라 특정 매서드를 서비스 매서드가 아니라, 필드나 매서드로 내가 지정하고 싶다면 선언식을 사용하면 도니다.

주석  : HTML, JSP, Java주석 다 사용가능.

HTMl <!-- --> , JSP <%-- -->, Java // or /* */ 

"각각 경우에 따라서 주석이 하는 역할 >> 주석이 주석일 때에  위치가 다를 수 있다."를 기억.

JavaScript의 기본문법을 이해한다.
DOM, Browser Event, Ajax이 각각 무엇인지 이해하고, 이를 활용해 웹화면을 제어할 수 있다.
JSP의 라이프사이클을 이해하고 redirect & forward 와 scope를 이해하고 사용할 수 있다. 
JSTL과 EL을 사용할 수 있다. 
데이터베이스를 설치하고 간단한 SQL을 사용할 수 있다. 
Maven을 이해하고 Maven을 이용한 웹 어플리케이션을 작성할 수 있다. 
JDBC 프로그래밍을 할 수 있다. 
Web API를 이해한다. 

의문점
main.jsp/mainServlet todoForm.jsp/todoFormServlet Todo


1. sql을 써서 테이블 연결을 하란거 보면 DB가 있긴 있다는 소린데 그럼 뭐가 데이터지? TO-DO-LIST들이? ㅇㅇ맞음
1-1. 조회, 삭제는 뭐지? done으로 넘어가기?...조회 삭제 항목은 필요없는건가
2. jsp를 쓰는것같던데 기존에 html과 css를 썼던 것처럼 그대로 jsp와 css를 쓰면 되나 
2-1. jsp와 html 차이가 뭐지 더 동적으로 페이지를 구현할 수 있게 해주는건가
3. 할일 등록 페이지에서 값 받는건 input이나 이런 걸로 받으면 될껏이다...
5. 카드 추가는.......어떤 함수를 만들어서 input에 값이 들어오면 새로운 카드를 만드는...건가보지?
6. 2개의 화면은 jsp로 구성하면 될 듯 하다. main.jsp/mainServlet todoForm.jsp/todoFormServlet
7. jQuery를 사용하지 않고, querySelector, addEventListener, innerHTML을 사용해서 DOM과 EVENT 처리를 하란다. 이게 뭐고 어디에 사용하는거지
8. Todo라는 이름의 maven 프로젝트로 생성하란다. 이게 뭐고 어디에 무슨 기능이 적용되는거지
9. 메인 화면을 위해서는 main.jsp와 MainServlet을 작성하란다. jsp는 알겠는데 mainservlet은 뭐냐 jsp가 서블릿으로 작동되는 거라매. 근데 먼 또 mainservlet이야 따로 servlet 파일을 생서해주는 ㄴ다
10. TodoDto 클래스와 TodoDao 클래스가 뭐지? main.jsp에 사용되어야하나 클래스?.....클래스가 뭐지......<%%> 안에 선언? 되어야 하는 건가 
10-1. TodoDto - Todo 테이블에 정보 한 건을 담을 수 있는 클래스 / TodoDao -  Todo 테이블에 입력, 수정, 조회하는 클래스
11. 새로운 todo등록 버튼을 클릭하면 해당 요청을 todoFormServlet서블릿이 받아서  todoForm.jsp 로 포워딩하여 할 일 등록 화면을 보여주기
12. 할일등록폼에서 제출버튼 누르면 post 방식? servlet때 getpost방식으로 처리하는 거 아는데 jsp에서는 어떻게 만드냐
13. ->를 누르면 id와 상태값을 전달한다음 success 를 보내라는데? id는 할일 등록될 때 알아서 등록되는건가
14. main.jsp에서 전달받은 결과를 JSTL과 EL을 이용해서 출력하라는데 JSTL, EL이 뭐임........
16. 할일등록 작성 후 제출 버튼을 누르면 post방식으로 TodoAddServlet로 값이 전달되고 여기서 TodoDao(이게 테이블 이름인가? ㄴㄴ 클래스 이름)를 이용해 테이블에 저장하고 메인화면 다시 주기

>210114
Maven이란?

Maven은 지금까지 애플리케이션을 개발하기 위해 반복적으로 진행해왔던 작업들을 지원하기 위하여 등장한 도구입니다. 
Maven을 사용하면 빌드(Build), 패키징, 문서화, 테스트와 테스트 리포팅, git, 의존성관리, svn등과 같은 형상관리서버와 연동(SCMs), 배포 등의 작업을 손쉽게 할 수 있습니다.
Maven을 이해하려면 CoC(Convention over Configuration)라는 단어를 먼저 이해해야 합니다.
CoC란 일종의 관습을 말하는데, 예를 들자면 프로그램의 소스파일은 어떤 위치에 있어야 하고, 소스가 컴파일된 파일들은 어떤 위치에 있어야 하고 등을 미리 정해놨다는 것입니다.
이 말은 관습에 이미 익숙한 사용자는 쉽게 Maven을 사용할 수 있는데, 관습에 익숙하지 않은 사용자는 이러한 제약사항에 대해서 심한 거부감을 느낄 수 있습니다.
Maven을 사용한다는 것은 어쩌면 이러한 관습 즉 CoC에 대해서 알아나가는 것이라고도 말할 수 있습니다. 



Maven을 사용할 경우 얻게 되는 이점은?
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


redirect는요. 클라이언트가 서버한테 요청을 보냈고요.그러면 이 서버는 어떤 일들을 처리하고 다시 어떻게 하냐면클라이언트한테 새로운 요청할 곳을 알려주면서 이걸로 다시 요청해요.

라고 주는 것이 리다이렉트에요.그래서 리다이렉트의 결과는 실제 실행한 다음에 url 주소가 바뀌었었던 거 혹시 기억하실까요? 그런데 포워드는요. 클라이언트는 요청을 보냈어요. 그런데 서버쪽에서 그 요청에 대해서 혼자 처리하는 것이 아니라 다른 누군가. back한테 처리를 맡기는 거죠. 이런 것을 포워드라고 하는데 이때 클라이언트는 이 서블릿, 요청받은 Servlet 1이 혼자서 다 처리해서 응답을 했는지 아니면 다른 누군가한테 부탁해서 처리를 했는지.
여기까지는 전혀 알 필요가 없어요.
그래서 포워드가 실행된 다음에는 url이 바뀌지 않아요.

```java
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            
            int diceValue = (int)(Math.random() * 6) + 1; 
            request.setAttribute("dice", diceValue);// 맡겨 놓을 수 있는 객체를 setAttribute라고 한다. diceValue는 세탁물이고, "dice"는 맡긴 이름. 나중에 "dice"라고 찾으면 diceValue값이 나온다. 

            RequestDispatcher requestDispatehcer = request.getRequestDispatcher("/next"); // 포워드하는 코드
            requestDispatehcer.forward(request, response);
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

