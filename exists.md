# EXISTS

<br />
<br />

* EXISTS 사용 이유?

---

```
EXISTS는 서브쿼리의 결과가 존재하는지 여부를 확인하는 데 사용되는 연산자이다.

주로 조건을 만족하는 행이 있는지 확인할 때 사용되며,
성능 최적화에 유리한 경우가 많다.
```

<br />
<br />
<br />
<br />

1. EXISTS 기본 개념

* EXISTS는 서브쿼리가 하나 이상의 행을 반환하면 TRUE를, 반환하지 않으면 FALSE를 반환한다.

* 서브쿼리의 실제 데이터 값은 중요하지 않으며, 단지 행이 존재하는지만 확인한다.

* EXISTS는 주로 상관 서브쿼리(Correlated Subquery)와 함께 사용된다.

<br />
<br />
<br />

2. 문법

```sql
SELECT column_name
  FROM table_name
 WHERE EXISTS (subquery);
```

<br />

| subquery | EXISTS |
|-|-|
| 조건을 확인하기 위한 내부 쿼리 | 서브쿼리가 결과를 반환하면 즉시 평가를 멈추므로 효율적 |

<br />
<br />
<br />

3. 특징

`성능`

```
EXISTS는 서브쿼리가 조건을 만족하는 첫 번째 행을 찾으면 더 이상 데이터를 읽지 않는다.

따라서 IN이나 JOIN보다 성능이 나을 수 있다.

정리하자면,
EXISTS는 서브쿼리의 결과가 존재하는지만 확인하므로,
대량 데이터에서 더 빠를 수 있다.

IN은 서브쿼리의 모든 값을 비교하므로,
데이터가 많을 경우 느려질 수 있다.
```

<br />

`상관 서브쿼리`

```
외부 쿼리의 값을 참조하는
서브쿼리와 자주 사용
```

<br />

`반대 연산`

```
NOT EXISTS를 사용해,
조건을 만족하는 행이 없는 경우를 확인할 수 있다.
```

<br />
<br />
<br />

4. 기본 사용

`orders 테이블에서 customers 테이블에 존재하는 고객의 주문만 조회하는 예시`

```sql
SELECT order_id, customer_id
FROM orders
WHERE EXISTS (
    SELECT 1
    FROM customers
    WHERE customers.customer_id = orders.customer_id
);

/* orders.customer_id와 일치하는 customers.customer_id가 있으면 해당 주문을 반환 */
```

<br />

`products 테이블에서 주문되지 않은 제품 조회 (NOT EXISTS)`

```sql
SELECT product_name
FROM products
WHERE NOT EXISTS (
    SELECT 1
    FROM order_details
    WHERE order_details.product_id = products.product_id
);

/* order_details에 해당 제품이 없으면 제품 이름을 반환 */
```
