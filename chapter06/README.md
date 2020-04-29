# 6장 데이터베이스 객체 작성과 삭제

## 26장 테이블 작성, 삭제, 변경

### CREATE TABLE로 테이블 작성하기

```sql
CREATE TABLE sample62(
    no INTEGER NOT NULL,
    a VARCHAR(30),
    b DATE);
)
```

> 결과

```sql
mysql> DESC sample62;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 데이터 행 삭제

> TRUNCATE TABLE [테이블명]


### ALTER TABLE로 테이블에 열 추가하기

> 명령어

```sql
ALTER TABLE sample62 ADD newcol INTEGER;
```

> 결과

```sql
DESC sample62;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| no     | int         | NO   |     | NULL    |       |
| a      | varchar(30) | YES  |     | NULL    |       |
| b      | date        | YES  |     | NULL    |       |
| newcol | int         | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

> ALTER TABLE ADD로 테이블에 열을 추가할 수 있다.

### ALTER TABLE로 열 속성 변경하기

> 명령어

```sql
ALTER TABLE sample62 MODIFY newcol VARCHAR(20);
```

> 결과

```sql
DESC sample62;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| no     | int         | NO   |     | NULL    |       |
| a      | varchar(30) | YES  |     | NULL    |       |
| b      | date        | YES  |     | NULL    |       |
| newcol | varchar(20) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### ALTER TABLE로 열 이름 변경하기

> 명령어

```sql
ALTER TABLE sample62 CHANGE newcol c VARCHAR(20);
```

> 결과

```sql
DESC sample62;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
| c     | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### ALTER TABLE로 열 삭제하기

> 명령어

```sql
ALTER TABLE smaple62 DROP c;
```

> 결과

```sql
DESC sample62;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

## 27장 제약

### 테이블 열에 제약 정의하기

> 명령어

```sql
CREATE TABLE sample631(
    a INTEGER NOT NULL,
    b INTEGER NOT NULL UNIQUE,
    c VARCHAR(30)
);
```

> 결과

```sql
 DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   |     | NULL    |       |
| b     | int         | NO   | PRI | NULL    |       |
| c     | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 테이블에 '테이블 제약' 정의하기

> 명령어

```sql
CREATE TABLE sample632(
    no INTEGER NOT NULL,
    sub_no INTEGER NOT NULL,
    name VARCHAR(30),
    PRIMARY KEY(no, sub_no)
);
```

> 결과

```sql
DESC sample632;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| no     | int         | NO   | PRI | NULL    |       |
| sub_no | int         | NO   | PRI | NULL    |       |
| name   | varchar(30) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### '테이블 제약'에 이름 부이기

> 명령어

```sql
CREATE TABLE sample632(
    no INTEGER NOT NULL,
    sub_no INTEGER NOT NULL,
    name VARCHAR(30),
    CONSTRAINT pkey_sample PRIMARY KEY(no, sub_no)
);
```

> 결과

```sql
 DESC sample632;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| no     | int         | NO   | PRI | NULL    |       |
| sub_no | int         | NO   | PRI | NULL    |       |
| name   | varchar(30) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 열 제약 추가하기

> 기존 테이블 

```sql
 DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   |     | NULL    |       |
| b     | int         | NO   | PRI | NULL    |       |
| c     | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```


> 명령어

```sql
ALTER TABLE sample631 MODIFY c VARCHAR(30) NOT NULL;
```

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   |     | NULL    |       |
| b     | int         | NO   | PRI | NULL    |       |
| c     | varchar(30) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 테이블 제약 추가하기

> 기존 테이블

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   |     | NULL    |       |
| b     | int         | NO   | PRI | NULL    |       |
| c     | varchar(30) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```


> 기본키 제약 추가하기

```sql
ALTER TABLE sample631 ADD CONSTRAINT pkey_sample631 PRIMARY KEY(a);
```

> 결과

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   | PRI | NULL    |       |
| b     | int         | NO   | UNI | NULL    |       |
| c     | varchar(30) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 제약 삭제

#### 열 제약 삭제하기

> 기존 테이블

```sql
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   | PRI | NULL    |       |
| b     | int         | NO   | UNI | NULL    |       |
| c     | varchar(30) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

> c 열의 NOT NULL 제약 없애기

```sql
ALTER TABLE sample631 MODIFY c VARCHAR(30);
```

> 결과

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   | PRI | NULL    |       |
| b     | int         | NO   | UNI | NULL    |       |
| c     | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 테이블 제약 삭제하기

> 기존 테이블

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   | PRI | NULL    |       |
| b     | int         | NO   | UNI | NULL    |       |
| c     | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

> pkey_sample631 제약 삭제하기

```sql
ALTER TABLE sample631 DROP CONSTRAINT pkey_sample631;
```

> my_sql의 경우

```sql
ALTER TABLE sample631 DROP PRIMARY KEY;
```

> 결과

```sql
DESC sample631;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| a     | int         | NO   |     | NULL    |       |
| b     | int         | NO   | PRI | NULL    |       |
| c     | varchar(30) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

### 기본키

#### sample634 테이블 작성하기

```sql
CREATE TABLE sample634(
    p INTEGER NOT NULL,
    a VARCHAR(30),
    CONSTRAINT pkey_sample634 PRIMARY KEY(p)
);
```

#### sample634에 행 추가하기

```sql
INSERT INTO sample634 VALUES(1, '첫째줄');
INSERT INTO sample634 VALUES(2, '둘째줄');
INSERT INTO sample634 VALUES(3, '셋째줄');
```

#### saple634에 중복하는 행 추가하기
```sql
INSERT INTO sample634 VALUES(2, '둘째줄');
```

> 결과

```sql
ERROR 1062 (23000): Duplicate entry '2' for key 'sample634.PRIMARY'
```

#### sample634을 중복된 값으로 갱신하기
```sql
UPDATE sample634 SET p=2 WHERE p=3;
```

```sql
ERROR 1062 (23000): Duplicate entry '2' for key 'sample634.PRIMARY'
```

## 29장 인덱스 작성과 삭제

## 30장 뷰 작성과 삭제



