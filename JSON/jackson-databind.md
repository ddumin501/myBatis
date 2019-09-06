
## JSON객체를 편하게 만드는 방법
jackson을 이용하면 번거로운 json객체를 쉽게 만들거나 String으로 변환할 수 있다.

```java
//Maver Repository에서 jackson databind 검색
//pom.xml에 추가한다.
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
	<version>2.9.8</version>
</dependency>
```
#### Test해보기
```java
//A.java (POJO)
public class A {
	private String str;
	private int num;
	private boolean flag;
	
	public String getStr() {
		return str;
	}
	public void setStr(String str) {
		this.str = str;
	}
	public int getNum() {
		return num;
	}
	public void setNum(int num) {
		this.num = num;
	}
	public boolean isFlag() {
		return flag;
	}
	public void setFlag(boolean flag) {
		this.flag = flag;
	}
}

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4NzA1NjYyMSw3MzA5OTgxMTZdfQ==
-->