# 예제용 데이터베이스 구축

> http://download.hanbit.co.kr/exam/2231/

해당 사이트로 가서 소스코드를 다운 받고 MySQL서버에 임포트해서 사용한다.

## 데이터 베이스 가져오기

> 명령어

```shell
mysql -uroot -p < [파일 위치]
```
위 명령어를 통해서 MySQL에 데이터 베이스를 import시킨다.

## 데이터 베이스 확인하기

> 명령어

```sql
show databases;
```
`show databases;`를 통해 MySQL에 저장되어 있는 데이터 베이스들을 확인할 수 있다.

> 결과

```sql
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sample             |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```

총 5개의 데이터 베이스가 있음을 확인 할 수 있다.

## 데이터 베이스 선택하기
>명령어

```sql
mysql> use sample
```
`use`명령어를 통해 사용하자 하는 데이터 베이스를 선택하면 된다.

> 결과

```sql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

## 확인해 보기

> 명령어

```sql
SELECT * FROM sample21;
```
SQL 명령어를 통하여 테이블을 확인해본다.

> 결과

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
SQL문을 통해 확인했을때 결과 값이 제대로 나왔으므로 문제없이 선택되었음을 볼 수 있다.