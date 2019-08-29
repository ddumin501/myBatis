## myBatis와 Spring 함께 쓰기
### 결과 
```java
   //OrderDAOOracle dao= new OrderDAOOracle(); 
   	String path = "beans.xml";
	  ApplicationContext ctx;
	  	ctx = new ClassPathXmlApplicationContext(path);
	  	
	  	OrderDAO dao = ctx.getBean("orderDAO", com.my.dao.OrderDAO.class);
```

**1. pom.xml에 다음 라이브러리 추가**

-mybatis-spring 라이브러리
```java
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.2</version>
    </dependency>
```
-spring-jdbc 라이브러리
```java
<!--https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.0.2.RELEASE</version>
    </dependency>
```
**2. beans.xml -> namespace**
mybatis-spring, spring-jdbc 추가

**3. beans.xml -> Source 추가**
```java
//dao 클래스 내부에 쓰일 property 지정
<bean id="orderDAO" class="com.my.dao.OrderDAOOracle">
		<property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
	</bean>

//myBatis에 쓰이는 seqlSessionFactory
<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
		<property name="configLocation"
			value="classpath:mybatis-config.xml"></property>
	</bean>

//jdbc에 필요한 정보
<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="oracle.jdbc.driver.OracleDriver">
		</property>
		<property name="url" value="jdbc:oracle:thin:@localhost:1521:xe" />
		<property name="username" value="ora_user" />
		<property name="password" value="password" />
	</bean>

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExMzQ4OTI0OSw4ODc5MTc1OTksMTQwMD
M3NTIwNCwxNTE3MDY1NTUsMTgwNjYwOTk0Myw1NTQyNTg1Miwt
MTAxODUwMDg2MCwxNzYwMDczMjcyLC04NDI0NzA0NjMsLTgyOT
A4NjUyNywtODg4NDM2NzgxXX0=
-->