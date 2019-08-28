


## Category
```sql
create table category(
cate_no number(1) CONSTRAINT category_pk PRIMARY KEY, 
cate_parent_no number(1),
cate_name varchar2(30) NOT NULL);

alter table category
add constraint category_parent_no_fk 
FOREIGN KEY(cate_parent_no) REFERENCES category(cate_no);

insert into category values (1, null, '음료');
insert into category values (2, null, '상품');
insert into category values (3, 1, '에스프레소');
insert into category values (4, 1, '콜드브루');
```
|cate_no[pk]|cate_parent_no| cate_name |
|--|--|--|
| 1 |null |음료  |
| 2 |null |상품  |
| 3 |1|에스프레소  |
| 4 |1|콜드브루 |

## Product
```sql
create table product(
 prod_no varchar(5),
 prod_cate_no number(1),
 prod_name varchar2(50),
 prod_price number(6) default 0 not null,
 prod_detail varchar2(50)
);

alter table product add constraint prod_no_pk primary key(prod_no)
add constraint prod_cate_fk foreign key(prod_cate_no) references category(cate_no)
add constraint prod_price_ck check(prod_price>=0);

insert into product values(10001,3,'플로랄 스타벅스 더블 샷',3000,null);
insert into product values(10002,3,'에스프레소 콘 파냐',3000,'풍부한 휘핑크림 음료');
insert into product values(10003,4,'나이트로 쇼콜라',4000,'초콜릿과 견과류의 풍미');
```
| prod_no | prod_cate_no | prod_name  | prod_price |prod_detail |
|--|--|--|--|--|
| 10001 |3 |플로랄 스타벅스 더블 샷  |3000  |null  |
| 10002 |3 |에스프레소 콘 파냐  |3000  | 풍부한 휘핑크림 음료 |
| 10003 |4 |나이트로 쇼콜라  |4000  | 초콜릿과 견과류의 풍미 |

## Order_Info
```sql
create table order_info(
order_no number,
order_id varchar2(15) not null,
order_time timestamp default systimestamp not null
);

alter table order_info 
add constraint order_no_pk primary key(order_no)
add constraint order_id_fk foreign key(order_id) references customer(id);
```
| order_no[pk] |order_id[fk] | order_time 
|--|--|--|
| 1 |id1 |8/28/10:23:00 |
| 2 |id9 |8/28/10:23:10 |
| 3 |id1 |8/28/11:00:00  |

## Order_Line
```sql
create table order_line(
order_no number,
order_prod_no varchar(5) not null,
order_quantity number(2) not null
);

alter table order_line 
add constraint order_line_pk primary key(order_no, order_prod_no),
add constraint order_no_fk foreign key(order_no) references order_info(order_no),
add constraint order_prod_fk foreign key(order_prod_no) references product(prod_no)
add constraint order_quantity_ck check(order_quantity between 1 and 99);

```
| order_no[pk][fk]|order_prod_no[pk][fk]| order_quantity
|--|--|--|
| 1 |10001 |2 |
| 1 |10003 |3 |
| 2 |10002 |1 |
| 3 |10002 |4 |

## 
```sql
CREATE SEQUENCE order_seq START WITH 1 INCREMENT BY 1 NOCACHE;
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDc4NzY2MjAsMTY3MDE2NDk3XX0=
-->