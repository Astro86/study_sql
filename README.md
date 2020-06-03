# SQL 첫걸음

- [My SQL 설치하기](setup.md)
- [1장 데이터 베이스 구축](chapter01/README.md)
- [2장 테이블에서 데이터 검색](chapter02/README.md)
- [3장 정렬과 연산](chapter03/README.md)
- [4장 데이터 추가, 삭제, 갱신](chapter04/README.md)
- [5장 집계와 서브쿼리](chapter05/README.md)
- [6장 데이터베이스 객체 작성과 삭제](chapter06/README.md)
- [7장 복수의 테이블 다루기](chapter07/README.md)

## JOIN

![](images/join.png)

- INNER JOIN : 두 테이블이 공통적으로 가지고 있는 레코드를 반환한다.
- LEFT JOIN : 두 테이블이 공통적으로 가지고 있는 레코드와 왼쪽 테이블의 모든 레코드를 반환한다.
- RIGHT JOIN : 두 테이블이 공통적으로 가지고 있는 레코드와 오른쪽 테이블의 모든 레코드를 반환한다.
- FULL OUTER JOIN : 두 테이블이 공통적으로 가지고 있는 레코드와 왼쪽 오른쪽 테이블의 레코드를 반환한다.

## SQL문 처리순서
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

원하는 테이블을 찾아가(FROM) 조건을 이용해 원하는 데이터를 검색한 후(WHERE) 그룹으로 묶은 뒤(GROUP BY) 그룹화된 데이터를 조건을 이용해 검색한 후(HAVING) 원하는 데이터를 선택해(SELECT) 정렬해서 내보낸다.(ORDER BY)

## 프로그래머스 sql문제

### select 문
- 모든 레코드 조회하기 https://programmers.co.kr/learn/courses/30/lessons/59034
- 역순 정렬하기 https://programmers.co.kr/learn/courses/30/lessons/59035
- 아픈 동물 찾기 https://programmers.co.kr/learn/courses/30/lessons/59036
- 어린 동물 찾기 https://programmers.co.kr/learn/courses/30/lessons/59037
- 동물의 아이디와 이름 https://programmers.co.kr/learn/courses/30/lessons/59403
- 여러 기준으로 정렬하기 https://programmers.co.kr/learn/courses/30/lessons/59404
- 상위 n개 레코드 https://programmers.co.kr/learn/courses/30/lessons/59405

### 집계함수 (SUM, MAX, MIN)
- 최댓 값 구하기 https://programmers.co.kr/learn/courses/30/parts/17043
- 최솟 값 구하 https://programmers.co.kr/learn/courses/30/lessons/59038
- 동물 수 구하기 https://programmers.co.kr/learn/courses/30/lessons/59406
- 중복 제거하기 https://programmers.co.kr/learn/courses/30/lessons/59408

### 그룹화 (GROUP BY)
- 고양이와 개는 몇마리 있을까 https://programmers.co.kr/learn/courses/30/lessons/59408
- 동명 동물 수 찾기 https://programmers.co.kr/learn/courses/30/lessons/59041
- 입양 시각 구하기 https://programmers.co.kr/learn/courses/30/lessons/59412
- 입양 시각 구하기2 https://programmers.co.kr/learn/courses/30/lessons/59413

### NULL 처리하기
- 이름이 없는 동물의 아이디 https://programmers.co.kr/learn/courses/30/lessons/59039
- 이름이 있는 동물의 아이디 https://programmers.co.kr/learn/courses/30/lessons/59407
- NULL 처리하기 https://programmers.co.kr/learn/courses/30/lessons/59410

### JOIN문
- 없어진 기록 찾기 https://programmers.co.kr/learn/courses/30/lessons/59042
- 있었는데요 없었습니다. https://programmers.co.kr/learn/courses/30/lessons/59043
- 오랜 기간 보호한 동물(1) https://programmers.co.kr/learn/courses/30/lessons/59044
- 보호소에서 중성화한 동물 https://programmers.co.kr/learn/courses/30/lessons/59045

### String, Date
- 루시와 엘라 찾기 https://programmers.co.kr/learn/courses/30/lessons/59046
- 이름에 el이 들어가는 동물 찾기 https://programmers.co.kr/learn/courses/30/parts/17047
- 중성화 여부 파악하기 https://programmers.co.kr/learn/courses/30/lessons/59409
- 오랜기간 보호한 동물(2) https://programmers.co.kr/learn/courses/30/lessons/59411
- DATETIME에서 DATE로 형 변환 https://programmers.co.kr/learn/courses/30/lessons/59414

