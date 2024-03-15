# mybatis에서 like를 사용하는 방법을 알아보자

<br />

1. MySQL
```sql
SELECT * 
FROM example
WHERE column LIKE CONCAT('%',#{parameter},'%') AND type = 0
LIMIT 1
```

<br />

2. Oracle
```sql
content like '%' ||  #{search} || '%'
```

<br />

3. MSSQL
```sql
content like '%' + #{search} + '%'
```
