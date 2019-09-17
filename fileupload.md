### 기본 페이지 구성만들기
form 태그를 만든다.
이때의 form태그의 property를 보면 enctype이 default값으로 들어있는데 이 default값 대신 multipart/form-data 형식으로 지정해줘야한다.
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

### library 다운받기
mvnrepository에 가서 servlets.com이 제공하는 cos를 다운받는다.
```java
<!-- https://mvnrepository.com/artifact/servlets.com/cos -->
<dependency>
    <groupId>servlets.com</groupId>
    <artifactId>cos</artifactId>
    <version>05Nov2002</version>
</dependency>
```

```java
//UpServlet
public class UpServlet extends HttpServlet {

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String saveDirectory = "files"; // tomcatserver 배포 directory의 files 폴더
		String realPath = getServletContext().getRealPath(saveDirectory);
		String encoding = "UTF-8";
		System.out.println(realPath);
		MultipartRequest mr= new MultipartRequest(request, realPath,encoding); //encoding이 추가된 생성자

	}

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODI2MzE1MzksLTM0OTQ5Mjk1NiwyND
Y2NDQ1NjAsLTE3NDU5Mjk5OTYsNTE2MDMwNjUxXX0=
-->