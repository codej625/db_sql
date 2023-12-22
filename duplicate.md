# GROUP BY를 사용하여 중복제거를 해보자!

<br/>

```sql
SELECT *
FROM ${table}
GROUP BY ${column}, ${column}, ${column} /* 중복제거 조건에 해당하는 컬럼들 */
ORDER BY ${colums} DESC /* 정렬 기준이 되는 컬럼 */
```
