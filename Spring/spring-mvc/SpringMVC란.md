
### DispatcherServlet 이 하는일
1) HandlerMapping: URL에 해당컨트롤 찾기
2) HandlerAdapter : 컨트롤러용 메서드 호출하기
(메서드매개변수를 요청전달데이터와 매핑, Command객체로 매핑, 요청전달데이터를 매개변수로 자동형변환
@ResponseBody가 설정되어있는 메서드는 문자열형태로 return
설정안된 메서드는 ModelAndView객체형태로 return

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0NjE5MDAzN119
-->