# MyBatis에서 datetime값을 Hashmap으로 받아보자

<br/>

```
datetime 타입의 칼럼값을 Hashmap으로 받으면,
1698236792000와 같은 타임스탬프 값으로 받아진다.
타임스탬프 값이 아닌 String 타입으로 받기 위해 필요한 명령어를 알아보자
```
ex) MyBatis XML
```sql
<select id="" parameterType="" resultType="hashmap">
  SELECT *, DATE_FORMAT(column_name, '%Y-%m-%d %H:%i:%s') AS column_name
  FROM   table_name
</select>
```
