
### DispatcherServlet 이 하는일
1) HandlerMapping : URL에 해당컨트롤 찾기
2) HandlerAdapter : 컨트롤러용 메서드 호출하기
-메서드매개변수를 요청전달데이터와 매핑, 
-Command객체로 매핑, 
-요청전달데이터를 매개변수로 자동형변환
@ResponseBody가 설정되어있는 메서드는 문자열형태로 return
설정안된 메서드는 ModelAndView객체형태로 return
3) ViewResolver :해당 View찾기
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
springmvc용 mvc1-
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwNDU5Mjg4N119
-->