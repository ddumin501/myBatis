
Spring Bean객체를 프로젝트가 Load될때 미리 만드는 작업이다.

```java
//web.xml에 추가
<!-- Bootstraps the root web application context before servlet initialization -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
```

Spring Bean Configure File을 새로 만든 후 
mvc-servlet.mxl에 있던 component-scan 구문과 bean 생성 구문을 옮겨온다.
```java
//applicationContext.xml

<context:annotation-config/>
<context:component-scan base-package="com.my.service"/>
	<context:component-scan base-package="com.my.dao"/>
	
	<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
		<property name="configLocation"
			value="classpath:mybatis-config.xml"></property>
	</bean>
	
	
	<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="oracle.jdbc.driver.OracleDriver">
		</property>
		<property name="url"
			value="jdbc:oracle:thin:@localhost:1521:xe" />
		<property name="username" value="ora_user" />
		<property name="password" value="password" />
	</bean>
```
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTI4MjExMDZdfQ==
-->