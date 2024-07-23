# SQL query 작성에 논리적 순서를 알아보자.

<br /><br />

1. SELECT 시

```
* 쿼리 작성 순서

1) SELECT: 반환할 열을 지정.

2) FROM: 데이터를 조회할 테이블을 지정.

3) WHERE: 필터링 조건을 지정.

4) GROUP BY: 그룹화할 열을 지정.

5) HAVING: 그룹화된 결과에 대한 필터링 조건을 지정.

6) ORDER BY: 정렬 조건을 지정.

7) LIMIT: 반환할 행의 수를 지정.
```

<br />

```sql
/* 쿼리 예시 */

SELECT
  name
  , department_id
  , AVG(salary) as avg_salary
FROM employees
WHERE department_id = 10
GROUP BY department_id, name
HAVING AVG(salary) > 50000
ORDER BY avg_salary DESC
LIMIT 10;
```

<br /><br /><br />

2. JOIN SELECT 시

```
* 쿼리 작성 순서

1) SELECT: 반환할 열을 지정.

2) FROM: 기본 테이블을 지정.

3) JOIN: 결합할 테이블을 지정.

4) ON: JOIN 조건을 지정.

5) WHERE: 필터링 조건을 지정.

6) GROUP BY: 그룹화할 열을 지정.

7) HAVING: 그룹화된 결과에 대한 필터링 조건을 지정.

8) ORDER BY: 정렬 조건을 지정.

9) LIMIT: 반환할 행의 수를 지정.
```

<br />

```sql
/* 쿼리 예시 */

SELECT
  A.name
  , B.salary
  , A.department_id
FROM employees A
INNER JOIN salaries B
ON A.employee_id = B.employee_id
WHERE A.department_id = 10
GROUP BY A.department_id, A.name, B.salary
HAVING AVG(B.salary) > 50000
ORDER BY B.salary DESC
LIMIT 10;
```
