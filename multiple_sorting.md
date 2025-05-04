# Multiple sorting

<br/>
<br/>

# 다중정렬의 순서?
```
ORDER BY를 사용해서 다중 정렬을 할 때,
왼쪽부터 차례대로 정렬되기 때문에 순서를 고려해야 한다.

즉, 우선 순위가 높은대로 정렬해야 한다.
```

<br/>
<br/>
<br/>
<br/>

```
예시 코드를 살펴보자.

1) 먼저 집합을 colums_1을 기준으로 오름차순으로 정렬한다.

2) 정렬 된 집합에서 column_2의 값을 기준으로 내림차순 정렬 한다.
(colums_1의 순서는 변하지 않고, column_2의 값만 변한다.)
```

```sql
SELECT *
FORM   {table}
ORDER  BY column_1 ASC, column_2 DESC;
```
