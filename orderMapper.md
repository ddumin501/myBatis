
## ResultMap
```java
<resultMap id="orderResultMap" type="OrderInfo"
		autoMapping="true">
		<id property="order_no" column="order_no" />
		<collection property="orderLines" ofType="OrderLine"
			autoMapping="true">
			<!-- id는 pk 역할.
					property 값이 다르면 OrderLine타입의 새객채를 생성 -->
			<!-- 	property값이 같으면 OrderLine타입의 기존객체 사용 -->
			<!-- id태그가 없으면 무조건 OrderLine타입의 새객체를 생성 -->
			<id property="order_no" column="order_no" />
			<id property="product.prod_no" column="order_prod_no" />
			<association property="product"
				javaType="com.my.vo.Product" autoMapping="true">
				<id property="prod_no" column="order_prod_no" />
			</association>
		</collection>
	</resultMap>

```sql
select info.order_no, info.order_time, line.order_prod_no, line.order_quantity,
p.prod_name, p.prod_price
from order_info info JOIN order_line line ON info.order_no = line.order_no
JOIN product p  ON p.prod_no = line.order_prod_no
WHERE order_id = #{id}
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0NTc3Mzc0NiwtNDE0MjY0OTM5LC0yMT
QzNzk3NDUyXX0=
-->