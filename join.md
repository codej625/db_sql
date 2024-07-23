# Join에 대해 알아보자.

<br /><br />

* 조인이란?
---

```
SQL에서 JOIN은 두 개 이상의 테이블을 결합하여,
관련 데이터를 조회할 때 사용된다. 
```

<br /><br /><br />

1. INNER JOIN

```
INNER JOIN은 두 테이블에서 일치하는 레코드만 반환한다.
```

<br />

```sql
SELECT A.name, B.salary
FROM employees A
INNER JOIN salaries B
ON A.employee_id = B.employee_id;

/* employees 테이블과 salaries 테이블에서 employee_id가 일치하는 레코드를 반환 */
```

<br /><br /><br />

2. LEFT JOIN (또는 LEFT OUTER JOIN)

```
LEFT JOIN은 왼쪽 테이블의 모든 레코드와 오른쪽 테이블의 일치하는 레코드를 반환하며,
일치하지 않는 경우 오른쪽 테이블의 값은 NULL로 채워진다.
```

<br />

```sql
SELECT A.name, B.salary
FROM employees A
LEFT JOIN salaries B
ON A.employee_id = B.employee_id;

/* employees 테이블의 모든 레코드와 salaries 테이블의 일치하는 레코드를 반환하며,
salaries 테이블에 일치하는 레코드가 없는 경우 NULL을 반환 */
```

<br /><br /><br />

3. RIGHT JOIN (또는 RIGHT OUTER JOIN)

```
RIGHT JOIN은 오른쪽 테이블의 모든 레코드와 왼쪽 테이블의 일치하는 레코드를 반환하며,
일치하지 않는 경우 왼쪽 테이블의 값은 NULL로 채워진다.
```

<br />

```sql
SELECT A.name, B.salary
FROM employees A
RIGHT JOIN salaries B
ON A.employee_id = B.employee_id;

/* salaries 테이블의 모든 레코드와 employees 테이블의 일치하는 레코드를 반환하며,
employees 테이블에 일치하는 레코드가 없는 경우 NULL을 반환 */
```

<br /><br /><br />

4. FULL JOIN (또는 FULL OUTER JOIN)

```
FULL JOIN은 두 테이블의 모든 레코드를 반환하며,
일치하지 않는 경우 해당 테이블의 값은 NULL로 채워진다.
```

<br />

```sql
SELECT A.name, B.salary
FROM employees A
FULL JOIN salaries B
ON A.employee_id = B.employee_id;

/* employees 테이블과 salaries 테이블의 모든 레코드를 반환하며,
일치하지 않는 레코드는 NULL을 포함 */
```

<br /><br /><br />

5. CROSS JOIN

```
CROSS JOIN은 두 테이블의 카르테시안 곱을 반환.
즉, 왼쪽 테이블의 각 행이 오른쪽 테이블의 각 행과 결합된다.
```

<br />

```sql
SELECT A.name, B.department
FROM employees A
CROSS JOIN departments B;

/* employees 테이블의 각 행을 departments 테이블의 각 행과 결합한 결과를 반환 */
```

<br /><br /><br />

6. SELF JOIN

```
SELF JOIN은 테이블 자체에 대해 JOIN을 수행.
이는 동일한 테이블의 두 개의 인스턴스를 결합하여 서로 다른 행을 비교할 때 유용하다.
```

<br />

```sql
SELECT A.name AS EmployeeName, B.name AS ManagerName
FROM employees A
INNER JOIN employees B
ON A.manager_id = B.employee_id;

/* employees 테이블을 두 번 사용하여 각 직원과 해당 직원의 매니저 이름을 반환 */
```

<br /><br />

```
각 JOIN의 종류는 특정 상황에 맞게 사용되며,
데이터베이스에서 데이터를 효과적으로 조작하고 조회하는 데 중요한 역할을 한다.
```
