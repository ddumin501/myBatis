
|  Aspect Oriented Programming | Object Oriented Programming |
|--|--|
| 재사용성을 높이자 | 재사용성을 높이자 |
|sop("before"); &nbsp;&nbsp; sop("before"); <br> a.a(); &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b.b(); <br> sop("after");| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parent(공통사항) <br>Child &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Child | 
|상속관계가 없다. 핵심사항의 위나 아래에 공통사항을 끼워넣음.|자식에게 고스란히 영향 끼침 -> 위험 多|
|공통사항과 핵심사항이 수평구조 | 공통사항과 핵심사항이 수직구조|

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NzQyODkxOSwtNzk3MDU1OTddfQ==
-->