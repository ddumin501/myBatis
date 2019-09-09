 ## Aspect Oriented Programming   VS   Aspect Oriented Programming
|  Aspect Oriented Programming |  Aspect Oriented Programming |
|--|--|
| 재사용성을 높이자 | 재사용성을 높이자 |
|공통사항(관점)<br>sop("before"); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; sop("before"); <br> a.a(); 핵심사항(관점)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b.b(); <br> sop("after");| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parent(공통사항) <br>Child &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child | 
|공통사항과 핵심사항이 수평구조 | 공통사항과 핵심사항이 수직구조|
|상속관계가 없다. <br>핵심사항과 공통사항의 관점 분리 형식.|자식에게 고스란히 영향 끼침 -> 위험 多|


##  Aspect Oriented Programming
공통사항(관심)과 핵심사항(관심)을 엮는다 - Weaving

-weaving방법
1) 핵심사항 컴파일시에 바이트코드에 공통사항을 추가
2) 핵심사항용 클래스로드시 바이트코드에 공통사항을 추가
3) 런타임시 프록시객체를 생성해서 공통사항을 추가 

sop("before") : 호출전에 처리되는 공통사항 -> (1)BeforeAdvice
sop("After") : 호출후에 처리되는 공통사항 -> (2)AfterAdvice
호출 
a() : 핵심사항 -> pointcut
a(), b(), c() : 핵심사항을 모아둔 것 -> joinpPoint
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyMjA4NDcwOSwtNzk3MDU1OTddfQ==
-->