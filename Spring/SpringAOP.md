
|  Aspect Oriented Programming | Object Oriented Programming |
|--|--|
| 재사용성을 높이자 | 재사용성을 높이자 |
|sop("before"); &nbsp;&nbsp; sop("before"); <br> a.a(); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b.b(); <br> sop("after");| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parent(공통사항) <br>Child &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child | 
|공통사항과 핵심사항이 수평구조 | 공통사항과 핵심사항이 수직구조|
|상속관계가 없다. <br>핵심사항과 공통사항의 관점 분리 형식.|자식에게 고스란히 영향 끼침 -> 위험 多|


공통사항(관심)과 핵심사항(관심)을 엮는다 - Weaving

-weaving방법
1) g
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU3MzA4Mjk1MCwtNzk3MDU1OTddfQ==
-->