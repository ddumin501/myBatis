
## JSON객체를 편하게 만드는 방법
jackson을 이용하면 Object 객체를 jsonString형식으로 쉽게 만들거나, 다시 Object로 변환 할 수 있다.

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
JSON String으로 변환 = mapper.writeValueAsString(Object);
Object 객체로 변환 = mapper.readValue(jsonSourcce, ObjectType);
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

------------------------console------------------------
{"str":"test","num":123,"flag":true}

test:123:true

[{"str":null,"num":1,"flag":false},{"str":null,"num":2,"flag":false},{"str":null,"num":3,"flag":false},{"str":null,"num":4,"flag":false},{"str":null,"num":5,"flag":false}]

null:1:false
null:2:false
null:3:false
null:4:false
null:5:false
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NTY0ODU3MjQsNzMwOTk4MTE2XX0=
-->