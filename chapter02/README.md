# 테이블에서 데이터 검색

```sql
use sample
```

## SELECT 명령어

```sql
SELECT * FROM sample21;
```

SELECT는 DML에 속하는 멸령으로 SQL에서 자주 사용된다.  
SELECT명령으로 데이터 베이스의 데이터를 읽어올 수 있다.  
`*`는 모든 열을 의미하는 `메타문자`이다.
FROM은 처리 대상 테이블을 지정하는 키워드

### 결과
```sql
+------+-----------+------------+---------------------------+
| no   | name      | birthday   | address                   |
+------+-----------+------------+---------------------------+
|    1 | 박준용    | 1976-10-18 | 대구광역시 수성구         |
|    2 | 김재진    | NULL       | 대구광역시 동구           |
|    3 | 홍길동    | NULL       | 서울특별시 마포구         |
+------+-----------+------------+---------------------------+
3 rows in set (0.00 sec)
```

NULL은 데이터 값으로 아무것도 저장되어 있지 않은 상태를 의미한다.


## DESC 명령어
```sql
DESC sample21;
```

테이블에 어떤 열이 정의도어 있는지 알 수 있다.

### 결과
```sql
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| no       | int         | YES  |     | NULL    |       |
| name     | varchar(20) | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| address  | varchar(40) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```
int : Integer를 의미한다.    
char(N) : 문자열형의 하나, 문자열을 저장할 수 있는 자료형이다. 문자열형에서는 열의 최대 길이를 저장해야 한다.  
VARCHAR : 문자열을 저장할 수 있는 자료형. 데이터 크기에 맞춰 저장공간의 크기도 변경된다.(가변 길이 문자열)  
DATE : 날짜값을 저장할 수 있는 자료형  
TIME : 시간을 저장할 수 있는 자료형  


Null : NULL 값을 허용할 것인지 아닌지를 나타내는 제약사항  
 - YES : NULL값을 허용  
 - NO : NULL값을 허용하지 않는다.  

Default : 열에 주어진 기본값(생략했을 경우 적용되는 값)





## WHERE 명령어

### 일치하는 결과값만 가져오기

```sql
 SELECT * FROM sample21 WHERE no = 2;
```
행 속에서 필요한 데이터만 검색하기 위한 명령어
WHERE구는 생략이 가능하다.

#### 결과
```sql
+------+-----------+----------+------------------------+
| no   | name      | birthday | address                |
+------+-----------+----------+------------------------+
|    2 | 김재진      | NULL     | 대구광역시 동구            |
+------+-----------+----------+------------------------+
1 row in set (0.00 sec)
```

### 제외하고 검색하기

```sql
 SELECT * FROM sample21 WHERE no <> 2;
```

#### 결과
```sql
+------+-----------+------------+---------------------------+
| no   | name      | birthday   | address                   |
+------+-----------+------------+---------------------------+
|    1 | 박준용    | 1976-10-18 | 대구광역시 수성구         |
|    3 | 홍길동    | NULL       | 서울특별시 마포구         |
+------+-----------+------------+---------------------------+
2 rows in set (0.00 sec)
```

### 문자열 검색하기
```sql
SELECT* FROM sample21 WHERE name='박준용';
```
`(' ')`작은 따옴표로 문자를 묶어서 검색해야 한다.

#### 결과
```sql
+------+-----------+------------+---------------------------+
| no   | name      | birthday   | address                   |
+------+-----------+------------+---------------------------+
|    1 | 박준용    | 1976-10-18 | 대구광역시 수성구         |
+------+-----------+------------+---------------------------+
1 row in set (0.00 sec)
```

### NULL값 검색하기
```sql
SELECT* FROM sample21 WHERE birthday IS NULL;
```
NULL인 행은 `=`연산자를 이용하여 검색할 수 없다.  
`IS NULL`을 이용하여 검색해야 한다.

```sql
+------+-----------+----------+---------------------------+
| no   | name      | birthday | address                   |
+------+-----------+----------+---------------------------+
|    2 | 김재진    | NULL     | 대구광역시 동구           |
|    3 | 홍길동    | NULL     | 서울특별시 마포구         |
+------+-----------+----------+---------------------------+
2 rows in set (0.00 sec)
```

## 조건 조합하기

### AND 연산자
```sql
SELECT * FROM sample24 WHERE a<>0 AND b<>0;
```
좌우의 식 모두 참일 경우 `AND` 연산자는 참을 반환한다.  
`모든 조건을 만족하는 경우 조건식은 참이된다`고 할때 `AND` 연산자로 조건식을 조합한다.  
`AND` 연산은 논리곱을 계산하는 논리 연산자이다.

#### 결과
```sql
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    4 |    2 |    2 |    0 |
+------+------+------+------+
1 row in set (0.00 sec)
```


### OR 연산자
```sql
SELECT* FROM sample24 WHERE no=1 OR no=2;
```
`어느 쪽이든 하나만 참이 되는 조건식은 참이 된다.`라고 할 경우 OR로 조건식을 연결한다.  
OR연산자는 논리합을 계산하는 논리 연산자이다.

```sql
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    1 |    1 |    0 |    0 |
|    2 |    0 |    1 |    0 |
+------+------+------+------+
2 rows in set (0.00 sec)
```

### NOT 연산자
```sql
SELECT* FROM sample24 WHERE NOT(a<>0 OR b<>0);
```
NOT연산자는 `단항 연산자`이다.


```sql
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    3 |    0 |    0 |    1 |
+------+------+------+------+
1 row in set (0.00 sec)
```

## 패턴 매칭에 의한 검색
특정 문자나 문자열이 포함되어 있는지를 검색하고 싶은 경우 사용한다.

### LIKE로 패턴 매칭하기

```sql
SELECT *  FROM sample25 WHERE text LIKE 'SQL%';
```
`LIKE`술어를 사용하면 열 값이 부분적으로 일치하는 경우에도 참이 된다.  
`%`, `_` 같은 특수 문자와 함께 사용한다.  
`%` : 임의의 문자열을 의미한다.  
`_` :임의의 문자 하나를 의미한다.  

```sql
+------+---------------------------------------------------+
| no   | text                                              |
+------+---------------------------------------------------+
|    1 | SQL은 RDBMS를 조작하기 위한 언어이다.             |
+------+---------------------------------------------------+
1 row in set (0.01 sec)
```
SQL로 시작하는 문자열을 검색했다.

```sql
SELECT* FROM sample25 WHERE text LIKE '%SQL%';
```

SQL이 들어간 문자열 모두를 검색한다.

```sql
+------+-----------------------------------------------------------------+
| no   | text                                                            |
+------+-----------------------------------------------------------------+
|    1 | SQL은 RDBMS를 조작하기 위한 언어이다.                           |
|    3 | LIKE는 SQL에서 사용할 수 있는 술어 중 하나이다.                 |
+------+-----------------------------------------------------------------+
2 rows in set (0.00 sec)
```

```sql
SELECT* FROM sample25 WHERE text LIKE '%\%%';
```

```sql
+------+------------------------------------------------------------+
| no   | text                                                       |
+------+------------------------------------------------------------+
|    2 | LIKE에서는 메타문자 %와 _를 사용할 수 있다.                |
+------+------------------------------------------------------------+
1 row in set (0.00 sec)
```