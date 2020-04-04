# 정렬과 연산

## 정렬하기 - ORDER BY

> 기존 테이블

```sql
mysql> SELECT * FROM sample31;
+------+------+---------------------------+
| name | age  | address                   |
+------+------+---------------------------+
| A씨  |   36 | 대구광역시 중구           |
| B씨  |   18 | 부산광역시 연제구         |
| C씨  |   25 | 서울특별시 중구           |
+------+------+---------------------------+
3 rows in set (0.00 sec)
```

### age를 기준으로 테이블 정렬하기

> 명령어

```sql
SELECT* FROM sample31 ORDER BY age;
```

나이를 기준으로 테이블`sample31`을 정렬하였다.

> 결과

```sql
+------+------+---------------------------+
| name | age  | address                   |
+------+------+---------------------------+
| B씨  |   18 | 부산광역시 연제구         |
| C씨  |   25 | 서울특별시 중구           |
| A씨  |   36 | 대구광역시 중구           |
+------+------+---------------------------+
3 rows in set (0.01 sec)
```

`오름차순`으로 정렬되었음을 확인할 수 있다.

### address를 기준으로 테이블 정리하기

> 명령어

```sql
SELECT* FROM sample31 ORDER BY address;
```

`address`를 기준으로 테이블을 정렬 시켰다.

> 결과

```sql
+------+------+---------------------------+
| name | age  | address                   |
+------+------+---------------------------+
| A씨  |   36 | 대구광역시 중구           |
| B씨  |   18 | 부산광역시 연제구         |
| C씨  |   25 | 서울특별시 중구           |
+------+------+---------------------------+
```

`사전순`으로 테이블이 정렬되었다.

## 내림 차순으로 정렬하기 - DESC

> 명령어

```sql
SELECT* FROM sample31 ORDER BY age DESC;
```

`DESC`를 붙임으로써 테이블을 내림차순으로 정렬한다.

> 결과

```sql
+------+------+---------------------------+
| name | age  | address                   |
+------+------+---------------------------+
| A씨  |   36 | 대구광역시 중구           |
| C씨  |   25 | 서울특별시 중구           |
| B씨  |   18 | 부산광역시 연제구         |
+------+------+---------------------------+
3 rows in set (0.00 sec)
```

## 오름 차순으로 정렬하기 - AES

> 명령어

```sql
SELECT* FROM sample31 ORDER BY age ASC;
```

`ASC`를 붙임으로써 테이블을 오름차순으로 정렬한다. `ASC`는 생략 가능

```sql
+------+------+---------------------------+
| name | age  | address                   |
+------+------+---------------------------+
| B씨  |   18 | 부산광역시 연제구         |
| C씨  |   25 | 서울특별시 중구           |
| A씨  |   36 | 대구광역시 중구           |
+------+------+---------------------------+
3 rows in set (0.00 sec)
```

## 복수의 열을 지정해 정렬하기

```sql
SELECT* FROM sample32 ORDER BY a;
```

#### 결과

```sql
+------+------+
| a    | b    |
+------+------+
|    1 |    1 |
|    1 |    3 |
|    1 |    2 |
|    2 |    1 |
|    2 |    2 |
+------+------+
5 rows in set (0.00 sec)
```

```sql
SELECT* FROM sample32 ORDER BY b,a;
```

#### 결과

```sql
+------+------+
| a    | b    |
+------+------+
|    1 |    1 |
|    2 |    1 |
|    1 |    2 |
|    2 |    2 |
|    1 |    3 |
+------+------+
5 rows in set (0.00 sec)
```

## 정렬방법 지정하기

```sql
SELECT* FROM sample32 ORDER BY a ASC, b DESC;
```

### 결과

```sql
+------+------+
| a    | b    |
+------+------+
|    1 |    3 |
|    1 |    2 |
|    1 |    1 |
|    2 |    2 |
|    2 |    1 |
+------+------+
5 rows in set (0.00 sec)
```

## 결과 행 제한하기 - LIMIT

> 테이블

```sql
+------+
| no   |
+------+
|    1 |
|    2 |
|    3 |
|    4 |
|    5 |
|    6 |
|    7 |
+------+
7 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT* FROM sample33 LIMIT 3;
```

> 결과

```sql
+------+
| no   |
+------+
|    1 |
|    2 |
|    3 |
+------+
3 rows in set (0.00 sec)
```

### 정렬 후 LIMIT로 행수 제한하기

> 명령어

```sql
SELECT* FROM sample33 ORDER BY no DESC LIMIT 3;
```

> 결과

```sql
+------+
| no   |
+------+
|    7 |
|    6 |
|    5 |
+------+
3 rows in set (0.00 sec)
```

### LIMIT를 사용할 수 없는 데이터베이스에서의 행 제한

> SQL Server

```sql
SELECT TOP 3 * FROM sample33;
```

> ORACLE

```sql
SELECT * FROM sample33 WHERE ROWNUM<=3;
```

## 오프셋 지정 - OFFSET

> 명령어

```sql
SELECT* FROM sample33 LIMIT 3 OFFSET 0;
```

## 수치 연산

> 기본 테이블

```sql
mysql> SELECT* FROM sample34;
+------+-------+----------+
| no   | price | quantity |
+------+-------+----------+
|    1 |   100 |       10 |
|    2 |   230 |       24 |
|    3 |  1980 |        1 |
+------+-------+----------+
3 rows in set (0.01 sec)
```

> 명령어

```sql
SELECT*, price*quantity FROM sample34;
```

> 결과

```sql
+------+-------+----------+----------------+
| no   | price | quantity | price*quantity |
+------+-------+----------+----------------+
|    1 |   100 |       10 |           1000 |
|    2 |   230 |       24 |           5520 |
|    3 |  1980 |        1 |           1980 |
+------+-------+----------+----------------+
3 rows in set (0.00 sec)
```

## 열의 별명 - AS

> 명령어

```sql
SELECT*, price*quantity AS amount FROM sample34;
```

> 결과

```sql
+------+-------+----------+--------+
| no   | price | quantity | amount |
+------+-------+----------+--------+
|    1 |   100 |       10 |   1000 |
|    2 |   230 |       24 |   5520 |
|    3 |  1980 |        1 |   1980 |
+------+-------+----------+--------+
3 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT*, price*quantity "금액" FROM sample34;
```

> 결과

```sql
+------+-------+----------+--------+
| no   | price | quantity | 금액   |
+------+-------+----------+--------+
|    1 |   100 |       10 |   1000 |
|    2 |   230 |       24 |   5520 |
|    3 |  1980 |        1 |   1980 |
+------+-------+----------+--------+
3 rows in set (0.00 sec)
```

## WHERE 구에서 계산, 검색하기

> 명령어

```sql
SELECT*, price*quantity AS amount FROM sample34 WHERE price*quantity >= 2000;
```

> 결과

```sql
+------+-------+----------+--------+
| no   | price | quantity | amount |
+------+-------+----------+--------+
|    2 |   230 |       24 |   5520 |
+------+-------+----------+--------+
1 row in set (0.00 sec)
```

> 명령어

```sql
SELECT*, price*quantity AS amount FROM sample34 WHERE amount >= 2000;
```

> 결과

```sql
ERROR 1054 (42S22): Unknown column 'amount' in 'where clause'
```

> 명령어

```sql
SELECT*, price*quantity AS amount FROM sample34 ORDER BY price*quantity DESC;
```

> 결과

```sql
+------+-------+----------+--------+
| no   | price | quantity | amount |
+------+-------+----------+--------+
|    2 |   230 |       24 |   5520 |
|    3 |  1980 |        1 |   1980 |
|    1 |   100 |       10 |   1000 |
+------+-------+----------+--------+
3 rows in set (0.01 sec)
```

> 명령어

```sql
SELECT*, price*quantity AS amount FROM sample34 ORDER BY amount DESC;
```

> 결과

```sql
+------+-------+----------+--------+
| no   | price | quantity | amount |
+------+-------+----------+--------+
|    2 |   230 |       24 |   5520 |
|    3 |  1980 |        1 |   1980 |
|    1 |   100 |       10 |   1000 |
+------+-------+----------+--------+
3 rows in set (0.01 sec)
```

## ROUND 함수 - 반올림

> 기존 테이블

```sql
SELECT* FROM sample341;
+---------+
| amount  |
+---------+
| 5961.60 |
| 2138.40 |
| 1080.00 |
+---------+
3 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT amount, ROUND(amount) FROM sample341;
```

> 결과

```sql
+---------+---------------+
| amount  | ROUND(amount) |
+---------+---------------+
| 5961.60 |          5962 |
| 2138.40 |          2138 |
| 1080.00 |          1080 |
+---------+---------------+
3 rows in set (0.00 sec)
```

### 소수점 둘째 자리에서 반올림하기

> 명령어

```sql
SELECT amount, ROUND(amount, 1) FROM sample341;
```

> 결과

```sql
+---------+------------------+
| amount  | ROUND(amount, 1) |
+---------+------------------+
| 5961.60 |           5961.6 |
| 2138.40 |           2138.4 |
| 1080.00 |           1080.0 |
+---------+------------------+
3 rows in set (0.00 sec)
```

### 10 단위를 반올림 하기

> 명령어

```sql
SELECT amount, ROUND(amount, -2) FROM sample341;
```

> 결과

```sql
+---------+-------------------+
| amount  | ROUND(amount, -2) |
+---------+-------------------+
| 5961.60 |              6000 |
| 2138.40 |              2100 |
| 1080.00 |              1100 |
+---------+-------------------+
3 rows in set (0.00 sec)
```

## 문자열 연산

### 문자열 결합 - CONCAT

```sql
SELECT CONCAT(quantity, unit) FROM sample35;
```

```sql
+------------------------+
| CONCAT(quantity, unit) |
+------------------------+
| 10개                   |
| 24통                   |
| 1장                    |
+------------------------+
3 rows in set (0.04 sec)
```

## CASE 문으로 데이터 변환하기

### CASE로 NULL 값을 0으로 변환하기

```sql
SELECT a, CASE WHEN a IS NULL THEN 0 ELSE a END "a(null=0)" FROM sample37;
```

```sql
+------+-----------+
| a    | a(null=0) |
+------+-----------+
|    1 |         1 |
|    2 |         2 |
| NULL |         0 |
+------+-----------+
3 rows in set (0.00 sec)
```

### COALESCE 함수를 이용한 NULL값 변환

```sql
SELECT a, COALESCE(a,0) FROM sample37;
```

```sql
+------+---------------+
| a    | COALESCE(a,0) |
+------+---------------+
|    1 |             1 |
|    2 |             2 |
| NULL |             0 |
+------+---------------+
3 rows in set (0.00 sec)
```

```sql
SELECT a AS "코드", CASE WHEN a=1 THEN '남자' WHEN a=2 THEN '여자' ELSE '미지정' END AS "성별" FROM sample37;
```

```sql
+--------+-----------+
| 코드   | 성별      |
+--------+-----------+
|      1 | 남자      |
|      2 | 여자      |
|   NULL | 미지정    |
+--------+-----------+
3 rows in set (0.00 sec)
```
