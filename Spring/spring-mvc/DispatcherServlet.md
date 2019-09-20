
### DispatcherServlet 이 하는일
1) HandlerMapping : URL에 해당컨트롤 찾기

2) HandlerAdapter : 컨트롤러용 메서드 호출하기
-메서드매개변수를 요청전달데이터와 매핑, 
-Command객체로 매핑, 
-요청전달데이터를 매개변수로 자동형변환
@ResponseBody가 설정되어있는 메서드는 문자열형태로 return
설정안된 메서드는 ModelAndView객체형태로 return

3) ViewResolver :해당 View찾기
**Controller에서 View로 이동하는 기본방법:forward
ex) @GetMapping("/a")
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; public String a( ){ return "/b.jsp"; }
**Controller에서 View로 이동하는 방법:redirect
ex) @GetMapping("/a")
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; public String a( ){ return "redirect : b.jsp"; }

web.xml파일 
```java
<servlet>
    <servlet-name>mvc1</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>mvc1</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
```
springMVC용 설정파일이름 :  mvc1-servlet.xml

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0ODYzNDUwNl19
-->