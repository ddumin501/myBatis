
```sql
select info.order_no, info.order_time, line.order_prod_no, line.order_quantity,
p.prod_name, p.prod_price
from order_info info JOIN order_line line ON info.order_no = line.order_no
J
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3OTE2OTU4Nl19
-->