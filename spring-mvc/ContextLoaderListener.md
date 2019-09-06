
Spring Bean객체를 프로젝트가 Load될때 미리 생성하게 하는 작업이다.

```java
//web.xml에 추가
<!-- Bootstraps the root web application context before servlet initialization -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
```

Spring Bean Configure File을 새로 만든 후 
mvc-servlet.mxl에 있던 비즈니스로직용 Bean을 옮겨온다.
```java
//applicationContext.xml

<context:annotation-config/>
   <!-- 비즈니스로직용 -->
   <context:component-scan base-package="com.my.service"/>
   <context:component-scan base-package="com.my.dao"/>
   
   
   <!-- 비즈니스로직용 -->
   <beans>
   <bean id="dataSource"
      class="org.springframework.jdbc.datasource.DriverManagerDataSource">
      <property name="driverClassName"
         value="oracle.jdbc.driver.OracleDriver">
      </property>
      <property name="url"
         value="jdbc:oracle:thin:@localhost:1521:xe">
      </property>
      <property name="username" value="c##oracle_user"></property>
      <property name="password" value="dmsk"></property>
   </bean>
   <!-- 비즈니스로직용 -->
   <bean id="sqlSessionFactory"
      class="org.mybatis.spring.SqlSessionFactoryBean">
      <property name="dataSource" ref="dataSource"></property>
      <property name="configLocation" value="classpath:mybatis-config.xml"/>
   </bean>
</beans>
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4MTkyMjAzNiwtMjAxMjgyMTEwNl19
-->