# GROUP BY를 사용하여 중복제거를 해보자!

<br/>

```sql
SELECT *
FROM ${table_name}
WHERE ${date_column} BETWEEN ${start_date} AND ${end_date}
GROUP BY ${column}, ${column}, ${column} /* 중복제거 조건에 해당하는 컬럼들 */
ORDER BY ${column} DESC /* 정렬 기준이 되는 컬럼 */
```
