 ## Aspect Oriented Programming   VS   Object Oriented Programming
|  Aspect Oriented Programming |  Object Oriented Programming |
|--|--|
| 재사용성을 높이자 | 재사용성을 높이자 |
|공통사항(관점)<br>sop("before"); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; sop("before"); <br> a.a(); 핵심사항(관점)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b.b(); <br> sop("after");| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parent(공통사항) <br>Child &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child | 
|공통사항과 핵심사항이 수평구조 | 공통사항과 핵심사항이 수직구조|
|상속관계가 없다. <br>핵심사항과 공통사항의 관점 분리 형식.|자식에게 고스란히 영향 끼침 -> 위험 多|


##  Aspect Oriented Programming
공통사항(관심)과 핵심사항(관심)을 엮는다 - Weaving

#### weaving방법
1) 핵심사항 컴파일시에 바이트코드에 공통사항을 추가
2) 핵심사항용 클래스로드시 바이트코드에 공통사항을 추가
3) 런타임시 프록시객체를 생성해서 공통사항을 추가 

#### 용어 정리 
-Advice
sop("before") : 호출전에 처리되는 공통사항 -> (1)BeforeAdvice
sop("After") : 호출후에 처리되는 공통사항 -> (2)AfterAdvice
호출 전후에 처리되는 공통사항 -> (3)AroundAdvice

a() : 핵심사항 -> pointcut
a(), b(), c() : 핵심사항을 모아둔 것 -> joinpPoint

## 선언적 트랜잭션 처리
```java
1) applicationContext.xml파일내용
<!-- 선언적 트랜잭션 -->	
<aop:aspectj-autoproxy/>
<bean id="transactionManager" 
      class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
  <property name="dataSource" ref="dataSource"/>
</bean>	
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
  <constructor-arg index="0" ref="sqlSessionFactory" />
</bean> 
<!--아래 설정 추가하세요!-->
<tx:annotation-driven transaction-manager="transactionManager"/>

2) AccountDAO.java에서 @Transactional어노테이션 설정 
@Repository
public class AccountDAO {
	@Autowired
	private SqlSession sqlSession;	
	@Transactional
	public void account(){
		HashMap<String, Object> map = new HashMap<>();
		String no1 ="101";
		map.put("no", no1);
		map.put("amount", 10);
		int rowCnt1 = 
			sqlSession.update("com.my.vo.Account.withdraw",map);
		if(rowCnt1 == 0) {
			throw new RuntimeException(no1+"계좌가 없어서 출금오류");
		}		
		map = new HashMap<>();
		//map.put("no", "102"); //
		
		String no2 = "999";
		map.put("no", no2); //
		map.put("amount", 10);

		//내부에서 uncheckedexception발생 - 자동롤백되어야한다.
		int rowCnt2 =sqlSession.update("com.my.vo.Account.deposit",	map);
		if(rowCnt2 == 0) {
			throw new RuntimeException(no1+"계좌가 없어서 입금오류");
		}
	}
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAwOTMwMTM3MiwtMTY5MTIxMTM5Niw4MT
M5MzAxODAsLTE2OTEyMTEzOTYsLTUwMjg1MDQwNCwtNzk3MDU1
OTddfQ==
-->