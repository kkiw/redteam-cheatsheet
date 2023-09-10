# mysql日常

### 0x0 查找数据中查找指定字段名所在的表

```sql
select * from INFORMATION_SCHEMA.columns where COLUMN_NAME Like '%placement%';
```

### 0x1 在特定数据库中查找

```sql
SELECT DISTINCT
	TABLE_NAME 
FROM
	INFORMATION_SCHEMA.COLUMNS 
WHERE
	COLUMN_NAME IN ( 'ColumnA', 'ColumnB' ) 
	AND TABLE_SCHEMA = 'DatabaseName';
```

```sql
SELECT DISTINCT
	TABLE_NAME 
FROM
	INFORMATION_SCHEMA.COLUMNS 
WHERE
	COLUMN_NAME LIKE '%ColumnA%' 
	AND TABLE_SCHEMA = 'DatabaseName';
```

### 0x2 在特定数据库中查找包含A和B字段的表

```sql
SELECT 
DISTINCT *  
FROM 
INFORMATION_SCHEMA.COLUMNS 
WHERE 
COLUMN_NAME IN ('A') 
and  TABLE_NAME in
    (SELECT 
    DISTINCT TABLE_NAME  
    FROM INFORMATION_SCHEMA.COLUMNS  
    WHERE 
    COLUMN_NAME IN ('B')  
    AND TABLE_SCHEMA='DatabaseName')
```

### 0x3 统计表行数

```sql
SELECT 
    table_name, 
    table_rows
FROM
    information_schema.tables
WHERE
    table_schema = 'dbname'
ORDER BY table_rows desc;
```

### 0x4  查找指定字段名所在的表，和表行数

```sql
SELECT
	a.TABLE_NAME,
	a.COLUMN_NAME,
	a.COLUMN_COMMENT,
	b.TABLE_ROWS 
FROM
	INFORMATION_SCHEMA.COLUMNS a
	LEFT JOIN information_schema.TABLES b ON a.TABLE_NAME = b.TABLE_NAME 
WHERE
	a.COLUMN_NAME LIKE '%phone%' 
ORDER BY
	b.TABLE_ROWS DESC;
	
```
