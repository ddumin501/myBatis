1. pom.xml에 다음 라이브러리 추가

**mybatis-spring 라이브러리**
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.2</version>
    </dependency>

**spring-jdbc 라이브러리**

    <!--https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.0.2.RELEASE</version>
    </dependency>

2. beans.xml -> namespace
mybatis-spring, spring-jdbc 추가
3. beans.xml 코드 추가
```java
<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="oracle.jdbc.drive.OracleDriver">
		</property>
		<property name="url"
	value="jdbc:oracle:thin:@localhost:1521:xe">
		</property>
		<property name="username" value="ora_user"></property>
		<property name="password" value="password"></property>
	</bean>
	<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
	</bean>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg0NDUyODkwMiwxNzYwMDczMjcyLC04ND
I0NzA0NjMsLTgyOTA4NjUyNywtODg4NDM2NzgxXX0=
-->