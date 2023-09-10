# mysql多表查询

### 多表left join 整合信息 并分页

```sql
SELECT *
FROM (
        SELECT TOP 10000 *
        FROM (
		select  top 10000 a.Posttime,a.Shipper,a.Shippertel,a.Shipperaddress,c.Goodname from orderinfo a 
		left join orderdetail b on a.Serialno=b.Serialno 
		left join goodinfo c on b.Goodinfoid =c.id
                ORDER BY a.Posttime DESC
            ) aa
        ORDER BY Posttime 
    ) bb
ORDER BY Posttime  DESC
```
