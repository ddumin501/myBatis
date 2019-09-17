form 태그를 만든다
이때의 form태그의 property를 보면 enctype이 default로 들어있는데 이 default 대신 multipart/form-data 형식으로 지정해줘야한다.
또한 무조건 get 방식으로 지정해주어야함
```html
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
```ㄴㄷㄱ
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NjMwMzkzNTQsLTE3NDU5Mjk5OTYsNT
E2MDMwNjUxXX0=
-->