# 🧠 SQL & 데이터베이스 암기노트

> 지금까지 배운 SQL / 데이터베이스 내용을 **시험·과제·복습용으로 빠르게 꺼내볼 수 있게** 암기 중심으로 정리한 노트

---

# 1. SQL 기본 구조

SQL은 데이터베이스에서 데이터를 만들고, 조회하고, 수정하고, 삭제하기 위한 언어이다.

가장 먼저 외울 기본 명령어:

```text
CREATE  = 만들기
DROP    = 구조 자체 삭제
INSERT  = 데이터 추가
SELECT  = 조회
UPDATE  = 수정
DELETE  = 데이터 삭제
```

---

# 2. CREATE TABLE

테이블을 새로 만들 때 사용한다.

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype
);
```

예:

```sql
CREATE TABLE customers (
    customer_id INTEGER,
    first_name VARCHAR(50),
    age INTEGER
);
```

암기:

> CREATE = 생성

---

# 3. DROP TABLE

테이블 자체를 삭제할 때 사용한다.

```sql
DROP TABLE customers;
```

중요:

> DROP TABLE = 테이블 구조 + 데이터 전체 삭제

---

# 4. DELETE FROM

테이블은 남겨두고 내부 데이터만 삭제할 때 사용한다.

```sql
DELETE FROM customers;
```

조건을 주면 일부 데이터만 삭제할 수 있다.

```sql
DELETE FROM customers
WHERE customer_id = 1;
```

---

## DROP TABLE vs DELETE FROM

| 구분 | DROP TABLE | DELETE FROM |
|---|---|---|
| 삭제 대상 | 테이블 자체 | 테이블 안의 데이터 |
| 테이블 구조 | 삭제됨 | 남아 있음 |
| 데이터 | 삭제됨 | 삭제됨 |
| WHERE 사용 | X | O |

암기:

> DROP = 집 자체 철거  
> DELETE = 집은 남기고 안의 물건만 삭제

---

# 5. INSERT INTO

테이블에 새 데이터를 추가할 때 사용한다.

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

예:

```sql
INSERT INTO customers (customer_id, first_name)
VALUES (1, 'Gayoung');
```

암기:

> INSERT = 데이터 넣기

---

# 6. SELECT

데이터를 조회할 때 사용한다.

```sql
SELECT column_name
FROM table_name;
```

여러 컬럼:

```sql
SELECT customer_id, first_name
FROM customers;
```

모든 컬럼:

```sql
SELECT *
FROM customers;
```

---

## SELECT * 의미

```sql
SELECT *
```

`*` = 모든 컬럼

암기:

> SELECT * = 전부 보여줘

---

# 7. UPDATE

기존 데이터를 수정할 때 사용한다.

```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

예:

```sql
UPDATE customers
SET age = 30
WHERE customer_id = 1;
```

주의:

> WHERE 없이 UPDATE하면 모든 행이 수정될 수 있다.

---

# 8. WHERE

조건에 맞는 데이터만 조회할 때 사용한다.

```sql
SELECT *
FROM customers
WHERE age >= 20;
```

자주 쓰는 비교 연산자:

```text
=   같다
!=  다르다
<>  다르다
>   초과
>=  이상
<   미만
<=  이하
```

---

# 9. AND / OR

조건을 여러 개 연결할 때 사용한다.

```sql
WHERE age >= 20
AND city = 'Seoul'
```

```sql
WHERE city = 'Seoul'
OR city = 'Incheon'
```

암기:

> AND = 둘 다 만족  
> OR = 하나만 만족해도 됨

---

# 10. ORDER BY

조회 결과를 정렬한다.

```sql
SELECT *
FROM customers
ORDER BY age;
```

기본값:

```text
ASC = 오름차순
```

내림차순:

```sql
ORDER BY age DESC;
```

암기:

```text
ASC  = 작은 값 → 큰 값
DESC = 큰 값 → 작은 값
```

---

# 11. DISTINCT

중복값을 제거해서 조회한다.

```sql
SELECT DISTINCT city
FROM customers;
```

암기:

> DISTINCT = 중복 제거 후 조회

---

# 12. GROUP BY

같은 값끼리 그룹으로 묶어서 집계할 때 사용한다.

```sql
SELECT city, COUNT(*)
FROM customers
GROUP BY city;
```

예:

> 도시별 고객 수

```sql
SELECT city, COUNT(*) AS customer_count
FROM customers
GROUP BY city;
```

암기:

> GROUP BY = 같은 값끼리 묶기

---

# 13. 집계 함수

자주 쓰는 집계 함수:

```text
COUNT = 개수
SUM   = 합계
AVG   = 평균
MAX   = 최대값
MIN   = 최소값
```

예:

```sql
SELECT AVG(price)
FROM products;
```

```sql
SELECT MAX(price)
FROM products;
```

---

# 14. HAVING

GROUP BY로 묶은 결과에 조건을 줄 때 사용한다.

```sql
SELECT city, COUNT(*)
FROM customers
GROUP BY city
HAVING COUNT(*) >= 10;
```

---

## WHERE vs HAVING

| 구분 | WHERE | HAVING |
|---|---|---|
| 조건 대상 | 개별 행 | 그룹 결과 |
| GROUP BY 전/후 | 전 | 후 |
| 집계 함수 조건 | 보통 X | O |

암기:

> WHERE = 묶기 전 조건  
> HAVING = 묶은 뒤 조건

---

# 15. JOIN

여러 테이블을 연결해서 조회할 때 사용한다.

기본 형태:

```sql
SELECT *
FROM table_a a
JOIN table_b b
    ON a.id = b.id;
```

---

# 16. INNER JOIN

양쪽 테이블에 모두 존재하는 데이터만 조회한다.

```sql
SELECT *
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;
```

암기:

> INNER JOIN = 둘 다 있는 것만

---

# 17. JOIN의 ON 절

`ON`은 두 테이블을 어떤 기준으로 연결할지 정한다.

예:

```sql
ON c.customer_id = o.customer_id
```

의미:

> customers 테이블의 customer_id와  
> orders 테이블의 customer_id가 같은 행끼리 연결

암기:

> ON = 연결 기준 키

---

# 18. 테이블 별칭(alias)

테이블 이름이 길 때 짧게 줄여 쓴다.

```sql
FROM products p
JOIN order_items oi
JOIN stock s
```

예:

```sql
p.product_id
oi.quantity
s.stock_quantity
```

주의:

> 별칭을 썼다면 어떤 컬럼이 어느 테이블 소속인지 확인해야 한다.

---

## 자주 헷갈린 별칭

```text
p  = products
oi = order_items
s  = stock
```

예:

```text
oi.quantity
```

→ 주문 수량

```text
s.stock_quantity
```

→ 재고 수량

암기:

> 같은 quantity처럼 보여도 어느 테이블 컬럼인지가 중요하다.

---

# 19. 서브쿼리(Subquery)

SQL문 안에 또 다른 SQL문을 넣는 방식이다.

예:

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

의미:

> 평균 가격보다 비싼 상품 조회

---

# 20. 평균보다 큰 값 찾기

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

암기 흐름:

```text
1. 안쪽 SELECT 실행
2. 평균값 계산
3. 바깥 SELECT에서 평균보다 큰 값 조회
```

---

# 21. MAX / MIN 서브쿼리

가장 비싼 상품:

```sql
SELECT *
FROM products
WHERE price = (
    SELECT MAX(price)
    FROM products
);
```

가장 싼 상품:

```sql
SELECT *
FROM products
WHERE price = (
    SELECT MIN(price)
    FROM products
);
```

---

# 22. EXISTS

서브쿼리 결과가 하나라도 존재하는지 확인한다.

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

의미:

> 주문 이력이 있는 고객

---

# 23. NOT EXISTS

서브쿼리 결과가 존재하지 않는 데이터를 찾는다.

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

의미:

> 주문 이력이 없는 고객

---

## EXISTS vs NOT EXISTS

```text
EXISTS     = 있으면
NOT EXISTS = 없으면
```

예:

```text
주문 이력이 있는 고객
→ EXISTS
```

```text
주문 이력이 없는 고객
→ NOT EXISTS
```

```text
한 번도 주문되지 않은 상품
→ NOT EXISTS
```

암기:

> 문제에 “없는 / 한 번도 ~하지 않은”이 나오면 NOT EXISTS를 먼저 떠올린다.

---

# 24. SELECT 1 in EXISTS

EXISTS 안에서는 실제 어떤 값을 SELECT하는지가 중요하지 않다.

```sql
SELECT 1
```

을 많이 사용한다.

예:

```sql
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

이유:

> EXISTS는 데이터 값 자체가 아니라  
> 조건에 맞는 행이 존재하는지만 확인하기 때문

암기:

> EXISTS 안의 SELECT 1 = “행이 있냐 없냐만 볼게”

---

# 25. NOT IN

특정 목록에 없는 값을 찾는다.

```sql
SELECT *
FROM products
WHERE product_id NOT IN (
    SELECT product_id
    FROM order_items
);
```

의미:

> 주문된 적 없는 상품

---

# 26. NOT IN vs NOT EXISTS

둘 다 “없는 데이터”를 찾을 때 사용할 수 있다.

### NOT IN

```sql
WHERE product_id NOT IN (...)
```

- 특정 값 목록에 없는지 비교
- NULL이 섞이면 예상치 못한 결과가 나올 수 있음

### NOT EXISTS

```sql
WHERE NOT EXISTS (...)
```

- 조건에 맞는 행 자체가 존재하는지 확인
- 관계형 데이터 비교에서 자주 사용

암기:

> NOT IN = 목록 안에 없냐  
> NOT EXISTS = 관련 행 자체가 없냐

---

# 27. DISTINCT vs NOT IN

둘은 완전히 다른 역할이다.

### DISTINCT

```sql
SELECT DISTINCT product_id
FROM order_items;
```

→ 중복 제거

### NOT IN

```sql
WHERE product_id NOT IN (...)
```

→ 목록에 없는 값만 조회

암기:

> DISTINCT = 중복 제거  
> NOT IN = 제외 조건

---

# 28. UNION

두 SELECT 결과를 합친다.

```sql
SELECT column_name
FROM table_a

UNION

SELECT column_name
FROM table_b;
```

특징:

> 중복 제거

---

# 29. UNION ALL

두 SELECT 결과를 합치되 중복도 유지한다.

```sql
SELECT column_name
FROM table_a

UNION ALL

SELECT column_name
FROM table_b;
```

---

## UNION vs UNION ALL

| 구분 | UNION | UNION ALL |
|---|---|---|
| 결과 합치기 | O | O |
| 중복 제거 | O | X |
| 중복 유지 | X | O |

암기:

> UNION = 합치고 중복 제거  
> UNION ALL = 전부 다 합치기

---

# 30. UNION 사용 조건

두 SELECT문의 컬럼 수가 같아야 한다.

예:

```sql
SELECT customer_id, name
FROM customers

UNION ALL

SELECT customer_id, name
FROM old_customers;
```

주의:

> 컬럼의 개수와 데이터 타입이 서로 호환되어야 한다.

---

# 31. SQL 실행 순서

작성 순서와 실제 처리 순서는 다르다.

작성:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

논리적 실행 순서:

```text
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
```

암기:

> FROM에서 가져오고  
> WHERE로 거르고  
> GROUP BY로 묶고  
> HAVING으로 그룹을 거르고  
> SELECT로 보여주고  
> ORDER BY로 정렬

---

# 32. SQL 대소문자

SQL 예약어는 일반적으로 대소문자를 구분하지 않는다.

둘 다 가능:

```sql
SELECT * FROM customers;
```

```sql
select * from customers;
```

하지만 가독성을 위해 보통 SQL 명령어는 대문자로 작성한다.

---

# 33. 문자열은 따옴표 사용

문자열 값은 작은따옴표로 감싼다.

```sql
WHERE city = 'Seoul'
```

숫자는 따옴표 없이 사용한다.

```sql
WHERE age = 30
```

---

# 34. NULL

NULL은 값이 없거나 알 수 없다는 뜻이다.

잘못된 방식:

```sql
WHERE column_name = NULL
```

올바른 방식:

```sql
WHERE column_name IS NULL
```

NULL이 아닌 값:

```sql
WHERE column_name IS NOT NULL
```

암기:

> NULL은 `=`가 아니라 `IS`

---

# 35. AS 별칭

컬럼 이름을 보기 좋게 바꿀 때 사용한다.

```sql
SELECT COUNT(*) AS customer_count
FROM customers;
```

`AS`는 생략할 수도 있다.

```sql
SELECT COUNT(*) customer_count
FROM customers;
```

---

# 36. COUNT(*) vs COUNT(column)

```sql
COUNT(*)
```

→ 전체 행 개수

```sql
COUNT(column_name)
```

→ 해당 컬럼에서 NULL을 제외한 값 개수

암기:

> COUNT(*) = 행 전체  
> COUNT(column) = NULL 제외

---

# 37. 데이터베이스 기본 개념

## Database

여러 데이터를 체계적으로 저장하고 관리하는 공간

## Table

행과 열로 구성된 데이터 저장 구조

## Row

하나의 데이터 레코드

## Column

데이터의 속성

예:

```text
customers
------------------------------------------------
customer_id | name | age | city
```

- Table = customers
- Column = customer_id, name, age, city
- Row = 고객 한 명의 정보

---

# 38. Primary Key

테이블에서 각 행을 유일하게 구분하는 키

예:

```text
customer_id
product_id
order_id
```

특징:

- 중복 X
- NULL X
- 한 행을 고유하게 식별

암기:

> PK = 주민등록번호처럼 한 행을 유일하게 구분

---

# 39. Foreign Key

다른 테이블의 Primary Key를 참조하는 키

예:

customers:

```text
customer_id
```

orders:

```text
customer_id
```

orders의 `customer_id`는 customers의 고객을 연결하는 역할을 한다.

암기:

> FK = 다른 테이블과 연결하는 다리

---

# 40. 관계형 데이터베이스

여러 테이블을 Key를 이용하여 서로 연결하는 데이터베이스 구조

예:

```text
customers
   ↓ customer_id
orders
   ↓ order_id
order_items
   ↓ product_id
products
```

이런 관계를 JOIN으로 연결해서 조회한다.

---

# 41. 자주 발생한 오류 패턴

## 테이블이 존재하지 않음

예:

```text
relation "..." does not exist
```

의미:

> SQL에서 참조한 테이블이 현재 데이터베이스에 없거나 이름이 다름

확인:

- 현재 DB가 맞는지
- 테이블 생성이 되었는지
- 테이블명이 정확한지
- 스키마가 맞는지

---

## 컬럼 이름 오류

예:

```text
column does not exist
```

확인:

- 컬럼명 철자
- 어느 테이블 소속 컬럼인지
- 별칭을 잘못 사용하지 않았는지

---

## 타입 오류

예:

```text
integer와 text 비교
```

확인:

- 컬럼 데이터 타입
- INSERT하는 값 타입
- JOIN 기준 컬럼 타입

---

# 42. SQL 문제 읽는 법

문제를 보면 먼저 핵심 단어를 찾는다.

```text
“모든” → SELECT *
“중복 없이” → DISTINCT
“~보다 큰” → WHERE >
“평균보다 큰” → 서브쿼리 + AVG
“가장 큰” → MAX
“가장 작은” → MIN
“~별” → GROUP BY
“그룹 중 조건” → HAVING
“정렬” → ORDER BY
“두 테이블 연결” → JOIN
“있는” → EXISTS
“없는 / 한 번도 없는” → NOT EXISTS
“결과 합치기” → UNION / UNION ALL
```

---

# 43. 문제 유형별 바로 떠올릴 문법

## 주문 이력이 없는 고객

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

## 한 번도 주문되지 않은 상품

```sql
SELECT *
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.product_id
);
```

---

## 평균보다 비싼 상품

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

---

## 가장 비싼 상품

```sql
SELECT *
FROM products
WHERE price = (
    SELECT MAX(price)
    FROM products
);
```

---

## 고객별 주문 수

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id;
```

---

## 주문 수가 3개 이상인 고객

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 3;
```

---

# 44. 자주 헷갈리는 개념 한방 비교

| 개념 | 의미 |
|---|---|
| DROP TABLE | 테이블 자체 삭제 |
| DELETE FROM | 테이블 안 데이터 삭제 |
| WHERE | 행 조건 |
| HAVING | 그룹 조건 |
| DISTINCT | 중복 제거 |
| NOT IN | 목록에 없는 값 조회 |
| EXISTS | 관련 행이 존재 |
| NOT EXISTS | 관련 행이 존재하지 않음 |
| UNION | 합치고 중복 제거 |
| UNION ALL | 전부 합치기 |
| INNER JOIN | 양쪽에 모두 있는 데이터 |
| GROUP BY | 같은 값끼리 묶기 |
| ORDER BY | 정렬 |
| SELECT * | 모든 컬럼 조회 |

---

# 45. 초압축 암기노트

```text
CREATE = 생성
DROP = 테이블 삭제
INSERT = 데이터 추가
SELECT = 조회
UPDATE = 수정
DELETE = 데이터 삭제

WHERE = 행 조건
GROUP BY = 묶기
HAVING = 그룹 조건
ORDER BY = 정렬

COUNT = 개수
SUM = 합계
AVG = 평균
MAX = 최대
MIN = 최소

JOIN = 테이블 연결
ON = 연결 기준
INNER JOIN = 둘 다 존재하는 데이터

DISTINCT = 중복 제거
EXISTS = 있음
NOT EXISTS = 없음
NOT IN = 목록에 없음

UNION = 합치고 중복 제거
UNION ALL = 전부 합치기

SELECT 1 = EXISTS에서 존재 여부만 확인

PK = 행을 유일하게 구분
FK = 다른 테이블과 연결

NULL = IS NULL / IS NOT NULL
```

---

# 46. 최종 암기 포인트

## SQL 기본 6개

```text
CREATE
DROP
INSERT
SELECT
UPDATE
DELETE
```

---

## 조회 흐름

```text
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

---

## 논리적 실행 순서

```text
FROM
→ WHERE
→ GROUP BY
→ HAVING
→ SELECT
→ ORDER BY
```

---

## 없는 데이터 찾기

```text
주문 이력 없는 고객
→ NOT EXISTS

한 번도 주문되지 않은 상품
→ NOT EXISTS
```

---

## EXISTS

```text
EXISTS = 존재 여부 확인
SELECT 1 = 값은 필요 없고 행 존재 여부만 확인
```

---

## JOIN

```text
JOIN = 테이블 연결
ON = 어떤 키로 연결할지 지정
```

---

## WHERE vs HAVING

```text
WHERE = 그룹화 전
HAVING = 그룹화 후
```

---

## UNION vs UNION ALL

```text
UNION = 중복 제거
UNION ALL = 중복 유지
```

---

## DROP vs DELETE

```text
DROP TABLE = 테이블 자체 삭제
DELETE FROM = 데이터만 삭제
```

---

## DISTINCT vs NOT IN

```text
DISTINCT = 중복 제거
NOT IN = 목록에 없는 값
```

---

# 47. 한 줄 암기

> **SQL은 FROM에서 데이터를 가져오고, WHERE로 거르고, GROUP BY로 묶고, HAVING으로 그룹을 거르고, SELECT로 보여주고, ORDER BY로 정렬한다.**

