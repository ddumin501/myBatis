## myBatis와 Spring 함께 쓰기

> ### myBatis 설정파일 찾기 과정 생략 가능
>  String resource = "mybatis-config.xml"; 		
>  InputStream inputStream; 		
> SqlSession session = null; 		
>inputStream = Resources.getResourceAsStream(resource); 			> SqlSessionFactory sqlSessionFactory = 
>new  SqlSessionFactoryBuilder().build(inputStream);


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
		<property name="dataSource" ref="dataSource"></property>
		<property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
	</bean>

//jdbc에 필요한 정보	
<bean id="dataSource"		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="oracle.jdbc.drive.OracleDriver">
		</property>
		<property name="url"
			value="jdbc:oracle:thin:@localhost:1521:xe">
		</property>
		<property name="username" value="ora_user"></property>
		<property name="password" value="password"></property>
	</bean>

//myBatis에 쓰이는 seqlSessionFactory
<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
		<property name="configLocation" value = "classpath"></property>
	</bean>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0NjE0MzM5NiwxODA2NjA5OTQzLDU1ND
I1ODUyLC0xMDE4NTAwODYwLDE3NjAwNzMyNzIsLTg0MjQ3MDQ2
MywtODI5MDg2NTI3LC04ODg0MzY3ODFdfQ==
-->