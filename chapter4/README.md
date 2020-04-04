# 데이터 추가, 삭제, 갱신

## 행 추가하기 - INSERT

> 명령어

```sql
SELECT * FROM sample41;
```

> 결과

```sql
Empty set (0.00 sec)
```

현재는 비어있는 테이블이다.

### sample41 열 구성 확인하기

> 명령어

```sql
DESC sample41;
```

> 결과

```sql
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

- no 열은 int(11)이므로 수치형 데이터를 저장할 수 있다.
- a 열은 varchar(30)이므로 최대 길이가 30인 문자열을 저장할 수 있다.
- b 열은 날짜 시간형 데이터를 저장할 수 있다.

### 행 추가 하기

> 명령어

```sql
INSERT INTO sample41 VALUES(1, 'ABC', '2014-01-25');
```

> 결과

```sql
Query OK, 1 row affected (0.00 sec)
```

### 확인하기

> 명령어

```sql
SELECT* FROM sample41;
```

> 결과

```sql
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
+----+------+------------+
1 row in set (0.00 sec)
```

### 값을 저장할 열 지정하기

> 명령어

```sql
INSERT INTO sample41(a, no) VALUES('XYZ', 2);
Query OK, 1 row affected (0.00 sec)
```

> 결과

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | NULL       |
+----+------+------------+
2 rows in set (0.00 sec)
```

### NOT NULL 제약

> 명령어

```sql
INSERT INTO sample41(no, a, b) VALUES(NULL, NULL, NULL);
ERROR 1048 (23000): Column 'no' cannot be null
```

행에 값이 없는 상태(NULL)로 두고 싶을 경우 VALUES구에서 NULL로 값을 지정할 수 있다.

> no 열에 대해서는 NULL값을 허용하지 않으므로 위 명령어는 에러가 발생한다.

> 명령어

```sql
INSERT INTO sample41(no, a, b) VALUES(3, NULL, NULL);
Query OK, 1 row affected (0.01 sec)
```

> 결과

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | NULL       |
|  3 | NULL | NULL       |
+----+------+------------+
3 rows in set (0.00 sec)
```

### DEFAULT에 대해 알아보기

> 명령어

```sql
DESC sample411;
```

> 결과

```sql
+-------+------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+------+------+-----+---------+-------+
| no    | int  | NO   |     | NULL    |       |
| d     | int  | YES  |     | 0       |       |
+-------+------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

sample411테이블 d 열에 대해서는 디폴트 값으로 0이 설정되어 있다.

#### 값을 생략하지 앟고 행 추가하기

> 명령어

```sql
INSERT INTO sample411(no, d) VALUES(1,1);
Query OK, 1 row affected (0.00 sec)
```

> 결과

```sql
SELECT * FROM sample411;
+----+------+
| no | d    |
+----+------+
|  1 |    1 |
+----+------+
```

#### DEFAULT로 값을 지정해 행 추가하기

> 명령어

```sql
INSERT INTO sample411(no, d) VALUES(2, DEFAULT);
Query OK, 1 row affected (0.00 sec)
```

> 결과

```sql
SELECT * FROM sample411;
+----+------+
| no | d    |
+----+------+
|  1 |    1 |
|  2 |    0 |
+----+------+
```

#### 암묵적으로 디폴트값을 가지는 행 추가하기

> 명령어

```sql
INSERT INTO sample411(no) VALUES(3);
Query OK, 1 row affected (0.00 sec)
```

> 결과

```sql
SELECT * FROM sample411;
+----+------+
| no | d    |
+----+------+
|  1 |    1 |
|  2 |    0 |
|  3 |    0 |
+----+------+
3 rows in set (0.00 sec)
```

열을 지정하지 않으면 디폴트값으로 행이 추가된다.

## 삭제하기 - DELETE

> 테이블

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | NULL       |
|  3 | NULL | NULL       |
+----+------+------------+
3 rows in set (0.00 sec)
```

`DELETE FROM sample41;`로 DELETE 명령을 실행하면 sample41 테이블의 모든 데이터가 삭제된다.

### 행 삭제하기

> 명령어

```sql
DELETE FROM sample41 WHERE no=3;
```

> 결과

```sql
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | NULL       |
+----+------+------------+
2 rows in set (0.00 sec)
```

> DELETE 명령은 WHERE 조건에 일치하는 `모든 행`을 삭제한다.

## 데이터 갱신하기 - UPDATE

> 테이블

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | NULL       |
+----+------+------------+
2 rows in set (0.00 sec)
```

DELETE와 달리UPDATE는 셀 단위로 데이터를 갱신할 수 있다.  
UPDATE 명령에서는 set구를 사용하여 갱신할 열과 값을 지정한다. `SET 열명 = 값` 이때 `=`는 비교연산자가 아닌, 값을 대입하는 대입 연산자이다.

> 명령어

```sql
UPDATE sample41 SET b = '2014-09-08' WHERE no=2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

> 결과

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2014-01-25 |
|  2 | XYZ  | 2014-09-08 |
+----+------+------------+
2 rows in set (0.00 sec)
```

> UPDATE 명령에서는 WHERE 조건에 일치하는 '모든 행'이 갱신된다.

### UPDATE 명령으로 증가 연산하기

> 명령어

```sql
UPDATE sample41 SET no = no+1;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0
```

> 결과

```sql
 SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  2 | ABC  | 2014-01-25 |
|  3 | XYZ  | 2014-09-08 |
+----+------+------------+
2 rows in set (0.00 sec)
```

모든 행의 no값에 1씩 더해진 것을 알 수 있다.

### 복수열 갱신

> 명령어

```sql
UPDATE sample41 SET a='xxx', b='2014-01-01' WHERE no=2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

콤마`,`로 구분하여 갱신할 열을 여러 개 지정할 수 있다.

> 결과

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  2 | xxx  | 2014-01-01 |
|  3 | XYZ  | 2014-09-08 |
+----+------+------------+
2 rows in set (0.00 sec)
```

### NULL로 갱신하기

> 명령어

```sql
UPDATE sample41 SET a=NULL;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0
```

> 결과

```sql
SELECT* FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  2 | NULL | 2014-01-01 |
|  3 | NULL | 2014-09-08 |
+----+------+------------+
2 rows in set (0.00 sec)
```

NOT NULL 제약이 설정되어 있는 열은 NULL이 허용되지 않는다.

## 물리 삭제와 논리 삭제

- 물리삭제 : SQL의 DELETE 명령을 사용해 직접 데이터를 삭제하는 방법
- 논리삭제 : 삭제 플래그와 같은 열을 미리 준비해 서 삭제 플레그의 값을 유효하게 갱신해두는 삭제 방법(실제 테이블안에 데이터는 남아있다.)
