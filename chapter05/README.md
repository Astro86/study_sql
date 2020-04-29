# 집계와 서브쿼리

## 행 개수 구하기 - COUNT

### COUNT로 행 개수 구하기

> 테이블

```sql
SELECT* FROM sample51;
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
|    3 | B    |       10 |
|    4 | C    |        3 |
|    5 | NULL |     NULL |
+------+------+----------+
5 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT COUNT(*) FROM sample51;
```

> 결과

```sql
+----------+
| COUNT(*) |
+----------+
|        5 |
+----------+
1 row in set (0.00 sec)
```

### 행 개수를 WHERE 구를 지정하여 구하기

> 테이블

```sql
SELECT* FROM sample51 WHERE name='A';
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
+------+------+----------+
2 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT COUNT(*) FROM sample51 WHERE name = 'A';
```

> 결과

```sql
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)
```

### 집계함수와 NULL값

> 명령어

```sql
SELECT COUNT(no), COUNT(name) FROM sample51;
```

> 결과

```sql
+-----------+-------------+
| COUNT(no) | COUNT(name) |
+-----------+-------------+
|         5 |           4 |
+-----------+-------------+
1 row in set (0.00 sec)
```

### DISTINCT로 중복 제거

> 테이블

```sql
SELECT* FROM sample51;
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
|    3 | B    |       10 |
|    4 | C    |        3 |
|    5 | NULL |     NULL |
+------+------+----------+
5 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT DISTINCT name FROM sample51;
```

```
+------+
| name |
+------+
| A    |
| B    |
| C    |
| NULL |
+------+
4 rows in set (0.00 sec)
```

### 집계함수에서 DISTINCT

> 명령어

```sql
SELECT COUNT(ALL name), COUNT(DISTINCT name) FROM sample51;
```

> 결과

```sql
+-----------------+----------------------+
| COUNT(ALL name) | COUNT(DISTINCT name) |
+-----------------+----------------------+
|               4 |                    3 |
+-----------------+----------------------+
1 row in set (0.00 sec)
```

## COUNT 이외의 집계함수

### SUM으로 합계 구하기

> 테이블

```sql
SELECT* FROM sample51;
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
|    3 | B    |       10 |
|    4 | C    |        3 |
|    5 | NULL |     NULL |
+------+------+----------+
5 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT SUM(quantity) FROM sample51;
```

> 결과

```sql
+---------------+
| SUM(quantity) |
+---------------+
|            16 |
+---------------+
1 row in set (0.00 sec)
```

### AVG로 평균내기

> 명령어

```sql
SELECT AVG(quantity), SUM(quantity)/COUNT(quantity) FROM sample51;
```

> 결과

```sql
+---------------+-------------------------------+
| AVG(quantity) | SUM(quantity)/COUNT(quantity) |
+---------------+-------------------------------+
|        4.0000 |                        4.0000 |
+---------------+-------------------------------+
1 row in set (0.01 sec)
```

### MIN, MAX로 최솟값, 최댓값 구하기

> 명령어

```sql
SELECT MIN(quantity), MAX(quantity), MIN(name), MAX(name) FROM sample51;
```

> 결과

```sql
+---------------+---------------+-----------+-----------+
| MIN(quantity) | MAX(quantity) | MIN(name) | MAX(name) |
+---------------+---------------+-----------+-----------+
|             1 |            10 | A         | C         |
+---------------+---------------+-----------+-----------+
1 row in set (0.00 sec)
```

## 그룹화 - GROUP BY

### GROUP BY로 그룹화

> 명령어

```sql
SELECT name FROM sample51 GROUP BY name;
```

> 결과

```sql
+------+
| name |
+------+
| A    |
| B    |
| C    |
| NULL |
+------+
4 rows in set (0.00 sec)
```

### name 열을 그룹화해 계산하기

> 명령어

```sql
SELECT name, COUNT(name), SUM(quantity) FROM sample51 GROUP BY name;
```

> 결과

```sql
+------+-------------+---------------+
| name | COUNT(name) | SUM(quantity) |
+------+-------------+---------------+
| A    |           2 |             3 |
| B    |           1 |            10 |
| C    |           1 |             3 |
| NULL |           0 |          NULL |
+------+-------------+---------------+
4 rows in set (0.00 sec)
```

### HAVING 구로 조건 지정

> 테이블

```sql
SELECT name, COUNT(name) FROM sample51 GROUP BY name;
+------+-------------+
| name | COUNT(name) |
+------+-------------+
| A    |           2 |
| B    |           1 |
| C    |           1 |
| NULL |           0 |
+------+-------------+
4 rows in set (0.00 sec)
```

> 명령어

```sql
SELECT name, COUNT(name) FROM sample51 GROUP BY name HAVING COUNT(name) = 1;
```

> 결과

```sql
+------+-------------+
| name | COUNT(name) |
+------+-------------+
| B    |           1 |
| C    |           1 |
+------+-------------+
2 rows in set (0.00 sec)
```

> 내부 처리 순서  
> WHERE 구 -> GROUP BY 구 -> HAVING 구 -> SELECT 구 -> ORDER BY 구

### 복수열의 그룹화

> 테이블

```sql
SELECT* FROM sample51;
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
|    3 | B    |       10 |
|    4 | C    |        3 |
|    5 | NULL |     NULL |
+------+------+----------+
5 rows in set (0.00 sec)
```

> GROUP BY를 사용할 때 주의할 점 : GROUP BY 에 지정한 열 이외의 열은 집계함수를 사용하지 않은 채 SELECT구에 기술해서는 안된다.

> 명령어

```sql
SELECT no, name, quantity FROM sample51 GROUP BY name;
```

> 결과

```sql
ERROR 1055 (42000): Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'sample.sample51.no' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by
```

GROUP BY로 그룹화 하면 클라이언트로 반환되는 결과는 그룹당 하나의 행이 된다. 하지만, name 열 값이 A인 그룹의 quantity 열 값은 1과 2로 두개이므로, 어떤 값을 반환할지 몰라 에러가 뜬다.

> 명령어

```sql
SELECT MIN(no), name, SUM(quantity) FROM sample51 GROUP BY name;
```

> 결과

```sql
+---------+------+---------------+
| MIN(no) | name | SUM(quantity) |
+---------+------+---------------+
|       1 | A    |             3 |
|       3 | B    |            10 |
|       4 | C    |             3 |
|       5 | NULL |          NULL |
+---------+------+---------------+
4 rows in set (0.00 sec)
```

### 결과 값 정렬

```sql
SELECT name, COUNT(name), SUM(quantity) FROM sample51 GROUP BY name ORDER BY SUM(quantity) DESC;
```

```sql
+------+-------------+---------------+
| name | COUNT(name) | SUM(quantity) |
+------+-------------+---------------+
| B    |           1 |            10 |
| A    |           2 |             3 |
| C    |           1 |             3 |
| NULL |           0 |          NULL |
+------+-------------+---------------+
4 rows in set (0.01 sec)
```

## 서브 쿼리

### DELETE의 WHERE 구에서 서브쿼리 사용하기

> 테이블

```sql
SELECT* FROM sample54;
+------+------+
| no   | a    |
+------+------+
|    1 |  100 |
|    2 |  900 |
|    3 |   20 |
|    4 |   80 |
+------+------+
4 rows in set (0.01 sec)
```

### 최솟값을 가지는 행 삭제하기

> 명령어

```sql
DELETE FROM sample54 WHERE a=(SELECT MIN(a) FROM sample54);
```

> 결과

```sql
ERROR 1093 (HY000): You can't specify target table 'sample54' for update in FROM clause
```

데이터를 추가하거나 갱신할 경우 동일한 테이블을 서브쿼리에서 사용할 수 없도록 되어 있기 때문에 이런 에러가 뜬다.

> 명령어

```sql
 DELETE FROM sample54 WHERE a=(SELECT a FROM(SELECT MIN(a) AS a FROM sample54) AS x);
```

> 결과

```sql
SELECT* FROM sample54;
+------+------+
| no   | a    |
+------+------+
|    1 |  100 |
|    2 |  900 |
|    4 |   80 |
+------+------+
3 rows in set (0.00 sec)
```

### 스칼라 값

#### 하나의 값을 반환하는 패턴

> 명령어

```sql
SELECT MIN(a) FROM sample54;
```

> 결과

```sql
+--------+
| MIN(a) |
+--------+
|     80 |
+--------+
1 row in set (0.00 sec)
```

#### 복수의 행이 반환되지만 열은 하나인 패턴

> 명령어

```sql
SELECT no FROM sample54;
```

> 결과

```sql
+------+
| no   |
+------+
|    1 |
|    2 |
|    4 |
+------+
3 rows in set (0.00 sec)
```

#### 하나의 행이 반환되지만 열이 복수인 패턴

> 명령어

```sql
SELECT MIN(a), MAX(no) FROM sample54;
```

> 결과

```sql
+--------+---------+
| MIN(a) | MAX(no) |
+--------+---------+
|     80 |       4 |
+--------+---------+
1 row in set (0.00 sec)
```

#### 복수의 행, 복수의 열이 반환되는 패턴

> 명령어

```sql
 SELECT no, a FROM sample54;
```

> 결과

```sql
+------+------+
| no   | a    |
+------+------+
|    1 |  100 |
|    2 |  900 |
|    4 |   80 |
+------+------+
3 rows in set (0.00 sec)
```

> SELECT 명령이 `하나의 값`만 반환하는 것을 `스칼라 값을 반환한다.`고 한다.

### SELECT 구에서 서브쿼리 사용하기

> 명령어

```sql
SELECT
    (SELECT COUNT(*) FROM sample51) AS sq1,
    (SELECT COUNT(*) FROM sample51) AS sq2;
```

My SQL에서는 FROM 구를 생략할 수 있다. 하지만 Oracle등 전통적인 데이터 베이스 제품에서는 FROM을 생략할 수 없습니다.

> 결과

```sql
+------+------+
| sq1  | sq2  |
+------+------+
|    5 |    5 |
+------+------+
1 row in set (0.00 sec)
```

### SET 구에서 서브쿼리 사용하기

> 명령어

```sql
UPDATE sample54 SET a = (SELECT a FROM (SELECT MAX(a) AS a FROM sample54)as x);
```

> 결과

```sql
SELECT* FROM sample54;
+------+------+
| no   | a    |
+------+------+
|    1 |  900 |
|    2 |  900 |
|    4 |  900 |
+------+------+
3 rows in set (0.00 sec)
```

## FROM 구에서 서브쿼리 사용하기

> 명령어

```sql
SELECT* FROM (SELECT* FROM sample54) sq;
```

> 결과

```sql
+------+------+
| no   | a    |
+------+------+
|    1 |  900 |
|    2 |  900 |
|    4 |  900 |
+------+------+
3 rows in set (0.00 sec)
```

## INSERT 명령과 서브쿼리

> 명령어

```sql
INSERT INTO sample541 VALUES(
    (SELECT COUNT(*) FROM sample51),
    (SELECT COUNT(*) FROM sample54)
);
```

> 결과

```sql
SELECT* FROM sample541;
+------+------+
| a    | b    |
+------+------+
|    5 |    3 |
+------+------+
1 row in set (0.00 sec)
```

### INSERT SELECT

> 명령어

```sql
INSERT INTO sample541 SELECT 1,2;
```

> 결과

```sql
SELECT* FROM sample541;
+------+------+
| a    | b    |
+------+------+
|    5 |    3 |
|    1 |    2 |
+------+------+
2 rows in set (0.00 sec)
```

## 상관 서브쿼리

### EXISTS

> 테이블

```sql
SELECT* FROM sample551;
+------+------+
| no   | a    |
+------+------+
|    1 | NULL |
|    2 | NULL |
|    3 | NULL |
|    4 | NULL |
|    5 | NULL |
+------+------+
```

> 테이블

```sql
SELECT* FROM sample552;
+------+
| no2  |
+------+
|    3 |
|    5 |
+------+
2 rows in set (0.00 sec)
```

sample 552 테이블에 있는지를 조사한 결과 값을 넣고 싶다.

> 명령어

```sql
UPDATE sample551 SET a = '있음' WHERE EXISTS (SELECT* FROM sample552 WHERE no2 = no);
```

```sql
SELECT* FROM sample551;
+------+--------+
| no   | a      |
+------+--------+
|    1 | NULL   |
|    2 | NULL   |
|    3 | 있음    |
|    4 | NULL   |
|    5 | 있음    |
+------+--------+
5 rows in set (0.00 sec)
```

### NOT EXISTS

> 명령어

```sql
UPDATE sample551 SET a = '없음' WHERE
    NOT EXISTS (SELECT* FROM sample552 WHERE no2 = no);
```

> 결과

```sql
SELECT* FROM sample551;
+------+--------+
| no   | a      |
+------+--------+
|    1 | 없음    |
|    2 | 없음    |
|    3 | 있음    |
|    4 | 없음    |
|    5 | 있음    |
+------+--------+
```

### 테이블 명 붙이기

양쪽 테이블에 동일한 이름의 열이 있을 경우 상관 서브 쿼리가 제대로 작동하지 않으므로 테이블 명을 붙일 필요가 있다.

```sql
UPDATE sample551 SET a = '있음' WHERE
    EXISTS (SELECT* FROM sample552 WHERE sample552.no2 = sample551.no);
```

### IN

집합 안의 값이 존재하는지를 조사할 수 있다.

> 명령어

```sql
SELECT* FROM sample551 WHERE no IN(3, 5);
```

> 결과

```sql
+------+--------+
| no   | a      |
+------+--------+
|    3 | 있음    |
|    5 | 있음    |
+------+--------+
```

#### IN의 오른쪽을 서브쿼리로 지정하기

> 명령어

```sql
SELECT* FROM sample551 WHERE no IN(SELECT no2 FROM sample552);
```

> 결과

```sql
+------+--------+
| no   | a      |
+------+--------+
|    3 | 있음    |
|    5 | 있음    |
+------+--------+
2 rows in set (0.00 sec)
```
