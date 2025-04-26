# Join

<br />
<br />

* 조인이란?
---

```
SQL 조인(JOIN)은 두 개 이상의 테이블에서 관련된 행들을 결합하여 하나의 결과 집합으로 만드는 데 사용된다.

조인을 통해 여러 테이블에 분산된 데이터를 효율적으로 조회할 수 있다.
```

<br />
<br />
<br />
<br />

`SQL 조인의 종류`

```
주요 SQL 조인 종류는 다음과 같다.

INNER JOIN (내부 조인)
LEFT JOIN (LEFT OUTER JOIN) (왼쪽 외부 조인)
RIGHT JOIN (RIGHT OUTER JOIN) (오른쪽 외부 조인)
FULL JOIN (FULL OUTER JOIN) (전체 외부 조인)
CROSS JOIN (교차 조인)`
```

```
밑에서 각 조인의 종류와 간단한 예시 코드를 살펴보자. 

* 예시를 위해 Customers 테이블과 Orders 테이블을 사용
```

<br />

`Customers`

|CustomerID|CustomerName|
|--------|--------------|
|1       |Alice         |
|2       |Bob           |
|3       |Charlie       |

`Orders`

|OrderID |CustomerID    |OrderDate |
|--------|--------------|----------|
|101	   |1        	    |2023-01-10|
|102	   |2	            |2023-01-15|
|103	   |1	            |2023-01-20|
|104	   |4	            |2023-01-25|

<br />
<br />
<br />

1. INNER JOIN (내부 조인)

```
INNER JOIN은 조인 조건에 맞는 양쪽 테이블의 행만 반환한다.

매칭되는 데이터만 가져오고,
어느 한쪽에만 존재하는 데이터는 제외된다.

* Customers 테이블과 Orders 테이블에서 CustomerID가 일치하는 행들만 가져온다.
```

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

`결과`

|CustomerName|OrderID|
|------------|-------|
|Alice	     |101    |
|Alice	     |103    |
|Bob	       |102    |

<br />
<br />
<br />

2. LEFT JOIN (LEFT OUTER JOIN) (왼쪽 외부 조인)

```
LEFT JOIN은 왼쪽 테이블의 모든 행과 오른쪽 테이블에서 조인 조건에 맞는 행을 반환한다.

오른쪽 테이블에서 일치하는 행이 없으면 해당 열은 NULL로 채워진다.

* Customers 테이블의 모든 고객 정보와 해당 고객의 주문 정보를 가져온다.
  주문이 없는 고객의 경우, 
  주문 정보 열은 NULL이 된다.
```

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

`결과`

|CustomerName|OrderID|
|------------|-------|
|Alice	     |101    |
|Alice	     |103    |
|Bob	       |102    |
|Charlie     |NULL   |

<br />
<br />
<br />

3. RIGHT JOIN (RIGHT OUTER JOIN) (오른쪽 외부 조인)

```
RIGHT JOIN은 오른쪽 테이블의 모든 행과 왼쪽 테이블에서 조인 조건에 맞는 행을 반환한다.

왼쪽 테이블에서 일치하는 행이 없으면 해당 열은 NULL로 채워진다.

* Orders 테이블의 모든 주문 정보와 해당 주문을 한 고객 정보를 가져온다.
  고객 정보가 없는 주문(예: CustomerID 4)의 경우, 
  고객 정보 열은 NULL이 된다.
```

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
RIGHT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

`결과`

|CustomerName|OrderID|
|------------|-------|
|Alice	     |101    |
|Alice	     |103    |
|Bob	       |102    |
|NULL        |104    |

<br />
<br />
<br />

4. FULL JOIN (FULL OUTER JOIN) (전체 외부 조인)

```
FULL JOIN은 왼쪽 또는 오른쪽 테이블 중 어느 한쪽에라도 존재하는 모든 행을 반환한다.

양쪽 테이블 모두에서 일치하는 행이 없는 경우,
해당 열은 NULL로 채워진다.

* Customers 테이블의 모든 고객 정보와 Orders 테이블의 모든 주문 정보를 가져온다.
  매칭되지 않는 경우에는 해당 열이 NULL이 된다.
```

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

`결과`

|CustomerName|OrderID|
|------------|-------|
|Alice	     |101    |
|Alice	     |103    |
|Bob	       |102    |
|Charlie	   |NULL   |
|NULL        |104    |

<br />
<br />
<br />

5. CROSS JOIN (교차 조인)

```
CROSS JOIN은 조인 조건 없이 양쪽 테이블의 모든 가능한 행 조합을 반환한다.

결과 집합의 행 수는 첫 번째 테이블의 행 수와 두 번째 테이블의 행 수를 곱한 값이 된다 (카티션 곱).

* Customers 테이블의 모든 고객과 Orders 테이블의 모든 주문을 가능한 모든 조합으로 연결한다.
  이 조인은 일반적으로 거의 사용되지 않으며,
  특정 분석이나 데이터 생성 목적 외에는 주의해서 사용해야 한다.
```

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
CROSS JOIN Orders;
```

`결과`

|CustomerName|OrderID|
|------------|-------|
|Alice	     |101    |
|Alice	     |102    |
|Alice	     |103    |
|Alice	     |104    |
|Bob	       |101    |
|Bob	       |102    |
|Bob	       |103    |
|Bob	       |104    |
|Charlie	   |101    |
|Charlie	   |102    |
|Charlie	   |103    |
|Charlie	   |104    |

```
결과 행 수는 Customers의 ROW * Orders의 ROW = 3 * 4 = 12
```

<br />
<br />
<br />

```
이 외에도 SELF JOIN이라고 하여 같은 테이블을 두 번 사용하여 조인하는 방식도 있지만,
이는 특별한 조인 종류라기보다는 INNER, LEFT, RIGHT 조인 등을 사용하여 자기 자신과 조인하는 방법이다.
```
