# mssql分页

### 利用排序的翻转拿到分页记录

```sql
SELECT *
FROM (
        SELECT TOP [每页记录] *
        FROM (
                SELECT TOP [每页记录*当前页数] [字段1, 字段2, ...]
                FROM [数据表]
                ORDER BY [排序字段] DESC
            ) [表别名1]
        ORDER BY [排序字段]
    ) [表别名2]
ORDER BY [排序字段] DESC
```
