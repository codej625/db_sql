# 뷰에 대해 알아보자.

<br /><br />

* VIEW
---

```
뷰(View)는 하나 이상의 테이블로부터 가져온 쿼리의 결과를 가상으로 나타내는 데이터베이스 객체이다.

뷰는 실제로 데이터를 저장하지 않고,
쿼리에 의해 동적으로 생성된 결과 집합을 나타낸다.
```

<br /><br /><br />

* 예시
```
두 개의 테이블이 있다고 가정
(오라클을 기준)
```

```
학생 테이블 (Students)

student_id (학생 ID)
student_name (학생 이름)
student_dob (학생 생년월일)
student_address (학생 주소)
```
```
성적 테이블 (Grades)

grade_id (성적 ID)
student_id (학생 ID, 외래 키)
subject (과목)
score (점수)
```
```
위에 두 개의 테이블을 조인하는 쿼리를 작성하고,
재사용이 가능한 뷰를 만들어보자.
```

<br />

```sql
/* 뷰 작성 */

CREATE VIEW StudentGrades AS
SELECT s.student_name, g.subject, g.score
FROM Students s
JOIN Grades g ON s.student_id = g.student_id;
```

```sql
/* SELECT 시 뷰 사용 */

SELECT * FROM StudentGrades;
```
