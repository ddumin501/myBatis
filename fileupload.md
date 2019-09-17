### 기본 페이
form 태그를 만든다
이때의 form태그의 property를 보면 enctype이 default로 들어있는데 이 default 대신 multipart/form-data 형식으로 지정해줘야한다.
또한 무조건 get 방식으로 지정해주어야함
```html
/* up.html */
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<form enctype = "multipart/form-data" 
	  action = "./up" 
      method = "post">
	<input name = "t" type="text"><br>
	<input name = "f1" type="file"><br>
	<input type = "submit" value="자료전송">
</form>
</body>
</html>
```

```java
//UpServlet.java

//import 생략
public class UpServlet extends HttpServlet {

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		InputStream is = request.getInputStream(); //http request의 message body를 읽어올 수 있음.
		InputStreamReader isr = new InputStreamReader(is);
		int readValue = -1;
		while((readValue=isr.read())!= -1) {
		System.out.print((char)readValue);
		}
	}

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzg5NjE4ODg3LDI0NjY0NDU2MCwtMTc0NT
kyOTk5Niw1MTYwMzA2NTFdfQ==
-->