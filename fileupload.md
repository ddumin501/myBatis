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
### 파일 업로드 Servlet 
```java
//UpServlet
public class UpServlet extends HttpServlet {

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
//		InputStream is = request.getInputStream(); //http request의 message body를 읽어올 수 있음.
//		InputStreamReader isr = new InputStreamReader(is);
//		int readValue = -1;
//		while((readValue=isr.read())!= -1) {
//		System.out.print((char)readValue);
//		}

		String saveDirectory = "files"; // tomcat server 배포 directory의 files 폴더
		String realPath = getServletContext().getRealPath(saveDirectory);
		int maxPostSize = 10 * 1024; // 10KB --업로드 될 수 있는 최대 파일크기 지정
		String encoding = "UTF-8";
		FileRenamePolicy policy = 
				new MyFileRenamePolicy(); //중복된 이름을 가진 파일이 올라갈 경우
		// MultipartRequest mr= new MultipartRequest(request, realPath,encoding); //encoding 매개변수 추가
		// MultipartRequest mr = new MultipartRequest(request, realPath, maxPostSize, encoding);// 파일크기 매개변수 추가
		MultipartRequest mr = new MultipartRequest(request, realPath, maxPostSize, encoding, policy); //policy변수 추가
	}

}
```
### 파일 이름 지정하기(중복 될 경우 덮어쓰기 방지)
```java
//FileRenamePolicy의 rename 메소드 오버라이딩 하기
public class MyFileRenamePolicy implements FileRenamePolicy{

	@Override
	public File rename(File file) {
		//System.out.println("rename("+ file +")호출");
		//1.파일이름 얻기
		System.out.println(file.getName()+", "+file.getAbsolutePath());
		
		String parent = file.getParent(); //현재파일의 부모파일까지의 경로
		String oldName = file.getName();
		System.out.println("parent :::::" + parent);
		
		//2.파일이름바꾸기 - yyMMddHHmmss
		//2-1. 확장자제외한 파일이름 얻기
		int extIdx = oldName.lastIndexOf(".");
		String name = oldName.substring(0, extIdx);
		//2-2. 이름에 yyMMddHHmmss이어붙이기
		SimpleDateFormat sdf = 
				new SimpleDateFormat("yyMMddHHmmss");
		String now = sdf.format(new java.util.Date());
		name = name + "_" + now;
		System.out.println("name:::::::"+name);
		//2-3. 이름과 확장자 이어붙이기
		String newName = name + oldName.substring(extIdx);
		//3.새파일 생성후 반환
		File f = new File(parent, newName);
		return f;
	}

}
```
### 파일 목록 불러오기
```java
public class ListServlet extends HttpServlet {

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// files 폴더에 있는 파일 목록 응답하기
		String realPath = getServletContext().getRealPath("files");
		System.out.println("files의 realPath::::::"+realPath);
		File files = new File(realPath);
		request.setAttribute("list", files.list());

		String path = "/listresult.jsp";
		RequestDispatcher rd = request.getRequestDispatcher(path);
		rd.forward(request, response);
	}
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzQ4NDUxNjA1LC0zNDA5OTgwMiwtMTc4Mj
YzMTUzOSwtMzQ5NDkyOTU2LDI0NjY0NDU2MCwtMTc0NTkyOTk5
Niw1MTYwMzA2NTFdfQ==
-->