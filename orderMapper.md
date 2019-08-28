
## ResultMap
```java
<!-- Very Complex Result Map -->
<resultMap id="detailedBlogResultMap" type="Blog">
	<constructor>
		<idArg column="blog_id" javaType="int" />
	</constructor>
	<result property="title" column="blog_title" />
	<association property="author" javaType="Author">
		<id property="id" column="author_id" />
		<result property="username" column="author_username" />
		<result property="password" column="author_password" />
		<result property="email" column="author_email" />
		<result property="bio" column="author_bio" />
		<result property="favouriteSection"
			column="author_favourite_section" />
	</association>
	<collection property="posts" ofType="Post">
		<id property="id" column="post_id" />
		<result property="subject" column="post_subject" />
		<association property="author" javaType="Author" />
		<collection property="comments" ofType="Comment">
			<id property="id" column="comment_id" />
		</collection>
		<collection property="tags" ofType="Tag">
			<id property="id" column="tag_id" />
		</collection>
		<discriminator javaType="int" column="draft">
			<case value="1" resultType="DraftPost" />
		</discriminator>
	</collection>
</resultMap>
```

```sql
select info.order_no, info.order_time, line.order_prod_no, line.order_quantity,
p.prod_name, p.prod_price
from order_info info JOIN order_line line ON info.order_no = line.order_no
JOIN product p  ON p.prod_no = line.order_prod_no
WHERE order_id = #{id}
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxNDI2NDkzOSwtMjE0Mzc5NzQ1Ml19
-->