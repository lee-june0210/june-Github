### SQL 문법 정리


<img src="https://user-images.githubusercontent.com/76678910/105009617-0a4b0580-5a7e-11eb-9f71-89d578bdfa57.png" width="60%" height="60%"></img>


```sql
SELECT * 
FROM  DEPARTMENT;

SELECT EMPNO, NAME, JOB
FROM EMPLOYEE;

SELECT CONCAT(EMPNO, '-', DEPTNO) AS '사번-부서번호'
FROM EMPLOYEE

SELECT DISTINCT DEPTNO
FROM EMPLOYEE;

```
<img src="https://user-images.githubusercontent.com/76678910/105007477-62ccd380-5a7b-11eb-96e9-0ace40abd86a.png" width="60%" height="60%"></img>
```
select name, deptno 
from employee 
where deptno in (10, 30);

select name, job 
from employee 
where name like '%A%';
```

<img src="https://user-images.githubusercontent.com/76678910/105007465-61031000-5a7b-11eb-95e1-c99cf208e616.png" width="60%" height="60%"></img>

```sql
SELECT EMPNO, NAME, JOB
FROM EMPLOYEE
ORDER BY NAME;

SELECT EMPNO AS 사번, NAME AS 이름, JOB AS 직업
FROM EMPLOYEE
ORDER BY 이름;

SELECT EMPNO, NAME, JOB
FROM EMPLOYEE
ORDER BY NAME DESC;


```

<img src="https://user-images.githubusercontent.com/76678910/105007473-62343d00-5a7b-11eb-80b4-a1c00f434af2.png" width="60%" height="60%"></img>

SELECT 구문 예제(함수의 사용)
```sql
UCASE, UPPER
mysql> SELECT UPPER('SEoul'), UCASE('seOUL');

from 다음에 테이블이 없을 경우에는 테이블에서 조회하는 것이 아닙니다.

LCASE, LOWER
mysql> SELECT LOWER('SEoul'), LCASE('seOUL');

substring
mysql> SELECT SUBSTRING('Happy Day',3,2);

LPAD, RPAD
mysql> SELECT LPAD('hi',5,'?'),LPAD('joe',7,'*');

TRIM, LTRIM, RTRIM
mysql> SELECT LTRIM(' hello '), RTRIM(' hello ');

SELECT deptno, AVG(salary) , SUM(salary)
FROM employee
group by deptno;

mysql> SELECT TRIM(' hi '),TRIM(BOTH 'x' FROM 'xxxhixxx');

ABS(x) : x의 절대값을 구합니다.
mysql> SELECT ABS(2), ABS(-2);

MOD(n,m) % : n을 m으로 나눈 나머지 값을 출력합니다.
mysql> SELECT MOD(234,10), 253 % 7, MOD(29,9);
```

### SQL_오류 모음

#### ORDER BY
```sql
ORDER BY NAME ASC, DATETIME DESC
```
이렇게 하면 NAME으로 먼저 정렬하고 NAME 중복되는 거에 한해서 DATETIME 정렬됨

#### SUB QUERY
```sql
SELECT NAME
FROM ANIMAL_INS
WHERE DATETIME = (SELECT MIN(DATETIME)
FROM ANIMAL_INS)
```

#### DISTINCT
```sql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
```

#### GROUP BY
```sql
SELECT NAME, COUNT(*) AS COUNT 
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) > 1
ORDER BY NAME
```
GROUP BY 할때는 HAVING으로 COUNT 걸어야함
	
#### WHERE
LIKE ‘%김’

#### CASE WHEN THEN END
```sql
SELECT ANIMAL_ID, NAME, CASE WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR SEX_UPON_INTAKE LIKE 'Spayed%' THEN 'O' ELSE 'X'END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```

컬럼명 잘보자

#### IN
```sql
WHERE user_id  IN ('user1','user3')

SELECT ANIMAL_ID, ANIMAL_TYPE, NAME
FROM ANIMAL_OUTS 
WHERE ANIMAL_ID IN ( 
SELECT ANIMAL_ID FROM ANIMAL_INS WHERE SEX_UPON_INTAKE LIKE 'Intact%'    )
AND SEX_UPON_OUTCOME NOT LIKE 'Intact%'
 ORDER BY ANIMAL_ID
```

#### SELF JOIN 대신 
```sql
 #1
SELECT     CART_ID
FROM    CART_PRODUCTS
WHERE CART_ID IN ( SELECT                    CART_ID
                   FROM                        CART_PRODUCTS
                   WHERE                        NAME = '우유')      AND NAME = '요거트'
ORDER BY CART_ID ASC;

#2
SELECT A.CART_ID FROM 
 (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '요거트') as A, 
 (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '우유') as B
 WHERE A.CART_ID = B.CART_ID
```

#### TIME
```sql
SELECT HOUR(DATETIME ) AS HOUR, COUNT(*) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >= 9 AND HOUR(DATETIME) < 20
GROUP BY HOUR
ORDER BY HOUR
```

#### TO_CHAR
```sql
SELECT ANIMAL_ID
     , NAME
     , TO_CHAR(DATETIME, 'YYYY-MM-DD') AS "날짜"
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID;
```
#### JOIN
```sql
SELECT JO.ANIMAL_ID, JO.NAME
FROM ANIMAL_INS AI JOIN ANIMAL_OUTS JO ON AI.ANIMAL_ID = JO.ANIMAL_ID	
WHERE AI.DATETIME > JO.DATETIME
ORDER BY AI.DATETIME
```
```sql
SELECT datetime
FROM (SELECT *
FROM ANIMAL_OUTS AO RIGHT OUTER JOIN ANIMAL_INS AI ON AO.ANIMAL_ID = AI.ANIMAL_ID
WHERE AO.ANIMAL_TYPE IS NULL) X
```
```sql
-- 코드를 입력하세요
SELECT *
FROM (
    SELECT AI.NAME, AI.DATETIME 
    FROM ANIMAL_INS AI LEFT OUTER JOIN ANIMAL_OUTS AO 
    ON AI.ANIMAL_ID = AO.ANIMAL_ID 
    WHERE AO.ANIMAL_ID IS NULL ORDER BY AI.DATETIME) N
WHERE ROWNUM <= 3 -- 아ㅏㅏㅏㅏㅏㅏ 이렇게 하면  3줄 먼저 짜르고 그다음에 ORDERBY 하네!!!!!!!


-- SELECT *
-- FROM(
-- SELECT A.NAME, A.DATETIME
-- FROM ANIMAL_INS A LEFT OUTER JOIN ANIMAL_OUTS B ON A.ANIMAL_ID=B.ANIMAL_ID
-- WHERE B.DATETIME IS NULL
-- ORDER BY A.DATETIME
-- )
-- WHERE ROWNUM<=3;
```
