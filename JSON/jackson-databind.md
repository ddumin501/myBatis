
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
```java
//Test.java
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;

public class Test {

	public static void main(String[] args) {
		A a = new A();
		a.setStr("test");
		a.setNum(123);
		a.setFlag(true);

		ObjectMapper mapper = new ObjectMapper();

		try {
			// POJO -> JSONString
			String jsonStr = mapper.writeValueAsString(a); // put method 필요 x
			System.out.println(jsonStr);
			System.out.println();
			
			// JSONString -> POJO
			A a1 = mapper.readValue(jsonStr, A.class);
			System.out.println(a1.getStr() + ":" + a1.getNum() + ":" + a1.isFlag());
			System.out.println();
			
			//List(POJO) -> JSONString
			List<A> list = new ArrayList<>();
			for (int i = 1; i <= 5; i++) {
				A a2 = new A();
				a2.setNum(i);
				list.add(a2);
			}
			String listJsonStr = mapper.writeValueAsString(list);
			System.out.println(listJsonStr);			
			System.out.println();
			
			//JSONString -> List(POJO)
			List<A> list1 = mapper.readValue(listJsonStr, new TypeReference<List<A>>() {});
			for(A a3 : list1) {
			System.out.println(a3.getStr() + ":" + a3.getNum() + ":" + a3.isFlag());
			}
			
		} catch (JsonProcessingException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzQxODk4NTgsNzMwOTk4MTE2XX0=
-->