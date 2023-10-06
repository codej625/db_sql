# MySQL 기준 특정 시간대를 기준으로 시간을 업데이트 시켜보자

```sql
UPDATE table_name
SET    date_column_name = DATE_ADD(date_column_name, INTERVAL 9 HOUR)
WHERE  date_column_name > '2023-09-30 23:17:03';
```
```
날짜가 들어있는 컬럼에 특정 시간대를 기준으로 9시간을 높여준다.
```
