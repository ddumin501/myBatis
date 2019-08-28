
## ResultMap
```java
<resultMap id="orderResultMap" type="OrderInfo"
		autoMapping="true">
		<id property="order_no" column="order_no" />
		<collection property="orderLines" ofType="OrderLine"
			autoMapping="true">
			<!--<id property="order_no" column="order_no" />
			<!-- property 값이 다르면 OrderLine타입의 새객채를 생성 -->
			<!-- property값이 같으면 OrderLine타입의 기존객체 사용 -->
			<!-- id태그가 없으면 무조건 OrderLine타입의 새객체를 생성 -->
			<id property="order_no" column="order_no" />
			<id property="product.prod_no" column="order_prod_no" />		
			<association property="product"
				javaType="com.my.vo.Product" autoMapping="true">
				<id property="prod_no" column="order_prod_no" />
			</association>
		</collection>
	</resultMap>
```

>  column은 SQL 결과의 header와 일치.  
>  property는 VO class의 변수명과 일치.    id는
> table의 pk역할을 한다.

 
**SELECT문**
```sql
select info.order_no, info.order_time, line.order_prod_no, line.order_quantity,
p.prod_name, p.prod_price
from order_info info JOIN order_line line ON info.order_no = line.order_no
JOIN product p  ON p.prod_no = line.order_prod_no
WHERE order_id = #{id}
```

-->결과

| ORDER_NO |ORDER_TIME  |ORDER_PROD_NO  |ORDER_PROD_QUANTITY  |PROD_NAME|PROD_PRICE|
|--|--|--|--|--|--|
2|	19/08/28 |15:27:54.035000000|10001|	2|플로랄 스타벅스 더블 샷|	3000
2|	19/08/28 |15:27:54.035000000|	10003	|3	|나이트로 쇼콜라|	4000
1|	19/08/28 |15:26:37.622000000|	10001|	2	|플로랄 스타벅스 더블 샷|	3000
1	|19/08/28| 15:26:37.622000000	|10003	|3|	나이트로 쇼콜라|	4000

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1MDU3NzAyLC02NzExMTU3MDIsMTc0NT
c3Mzc0NiwtNDE0MjY0OTM5LC0yMTQzNzk3NDUyXX0=
-->