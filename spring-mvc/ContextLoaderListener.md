
Spring Bean객체를 프로젝트가 Load될때 미리 만드는 작업이다.

```java
//web.xml에 추가
<!-- Bootstraps the root web application context before servlet initialization -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE5NDg1ODMwXX0=
-->