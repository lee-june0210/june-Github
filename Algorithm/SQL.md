# SQL

#### SQL 배치순서
<img src ="https://user-images.githubusercontent.com/76678910/109505381-e26caa00-7adf-11eb-93eb-3c495264b825.PNG"></img>

### SQL 문법 정리

#### SELECT 문 예시
```sql

SELECT CONCAT(EMPNO, '-', DEPTNO) AS '사번-부서번호'
FROM EMPLOYEE
```
```SQL
SELECT DISTINCT DEPTNO
FROM EMPLOYEE;
```
<img src="https://user-images.githubusercontent.com/76678910/105007477-62ccd380-5a7b-11eb-96e9-0ace40abd86a.png" width="60%" height="60%"></img>
```sql
select name, deptno 
from employee 
where deptno in (10, 30);
```
```
select name, job 
from employee 
where name like '%A%';
```
```
WHERE INTAKE_CONDITION NOT IN ('Aged')
WHERE INTAKE_CONDITION <> 'Aged'
```

<img src="https://user-images.githubusercontent.com/76678910/105007465-61031000-5a7b-11eb-95e1-c99cf208e616.png" width="60%" height="60%"></img>
#### NAME 순서대로 = 기본 / 역순으로,  = DESC 
```sql

SELECT EMPNO AS 사번, NAME AS 이름, JOB AS 직업
FROM EMPLOYEE
ORDER BY 이름;
```
```
SELECT EMPNO, NAME, JOB
FROM EMPLOYEE
ORDER BY NAME DESC;


```

<img src="https://user-images.githubusercontent.com/76678910/105007473-62343d00-5a7b-11eb-80b4-a1c00f434af2.png" width="60%" height="60%"></img>

SELECT 구문 예제(함수의 사용)
```sql
from 다음에 테이블이 없을 경우에는 테이블에서 조회하는 것이 아닙니다.

UPPER
mysql> SELECT UPPER('SEoul');

LOWER
mysql> SELECT LOWER('SEoul');

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

#### DISTINCT
```sql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
```
#### NVL
* NVL(column,"str")
column이 null이면 "str" 반환 


#### TIME
```sql
SELECT HOUR(DATETIME ) AS HOUR, COUNT(*) AS COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >= 9 AND HOUR(DATETIME) < 20
GROUP BY HOUR
ORDER BY HOUR
```
```
SELECT ANIMAL_ID
     , NAME
     , TO_CHAR(DATETIME, 'YYYY-MM-DD') AS "날짜"
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID;
```
```
select ao.animal_id as ANIMAL_ID, ai.name as NAME
from animal_outs ao join animal_ins ai on out_ani.animal_id = in_ani.animal_id
order by ao.datetime - ai.datetime desc
limit 2
```
```
SELECT animal_id, name from (select a.animal_id, a.name, (b.datetime-a.datetime) as cha                                  
				from animal_ins a, animal_outs b 
                                 where a.animal_id = b.animal_id
                                 order by 3 desc)
where rownum < 3 ;
```

#### NULL

* NVL(표현식1, 표현식2) 
표현식1의 결과값이 NULL이면 표현식2의 값을 출력

* ISNULL(표현식1, 표현식2)  
표현식1의 결과값이 NULL이면 표현식2의 값을 출력

* NULLIF(표현식1,표현식2)  
표현식1이 표현식2와 같으면 NULL을, 같지 않으면 표현식1을 리턴

```SQL
SELECT ANIMAL_TYPE, nvl(name, 'No name') AS NAME, SEX_UPON_INTAKE
from ANIMAL_INS
ORDER BY ANIMAL_ID
```

#### CASE WHEN THEN END
<img src ="https://user-images.githubusercontent.com/76678910/109624291-62971c00-7b81-11eb-87d0-2c0c424c7fbb.PNG"></img>
```sql
SELECT ANIMAL_ID, NAME, 
	CASE WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR SEX_UPON_INTAKE LIKE 'Spayed%' 
		THEN 'O' 
		ELSE 'X'
	END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```
CASE WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR 'Spayed%' 이렇게 하면 다른 값 나옴. 저 위에가 맞

컬럼명 잘보자

#### limit
* mysql에서만 사용가능
* where 절없이 바로 사용 가능
ORACLE에서는 ROWNUM쓰라는데 프로그래머스에서 안먹넹
```sql
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 
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

#### IN
```sql
WHERE user_id  IN ('user1','user3')

SELECT ANIMAL_ID, ANIMAL_TYPE, NAME
FROM ANIMAL_OUTS 
WHERE ANIMAL_ID IN (SELECT ANIMAL_ID 
		    FROM ANIMAL_INS 
		    WHERE SEX_UPON_INTAKE LIKE 'Intact%')
AND SEX_UPON_OUTCOME NOT LIKE 'Intact%'
 ORDER BY ANIMAL_ID
```
#### SUB QUERY
```sql
SELECT NAME
FROM ANIMAL_INS
WHERE DATETIME = (SELECT MIN(DATETIME)
		  FROM ANIMAL_INS)
```
```SQL
SELECT AI.ANIMAL_ID, AI.ANIMAL_TYPE, AI.NAME
FROM ANIMAL_INS AI JOIN (SELECT ANIMAL_ID 
			FROM  ANIMAL_OUTS 
			WHERE SEX_UPON_OUTCOME LIKE 'Neutered%' OR SEX_UPON_OUTCOME LIKE 'Spayed%'
			) X ON AI.ANIMAL_ID = X.ANIMAL_ID
WHERE AI.SEX_UPON_INTAKE LIKE 'Intact%'
ORDER BY AI.ANIMAL_ID
```
```SQL
SELECT C.CART_ID
FROM CART_PRODUCTS C JOIN (SELECT CART_ID, NAME
                    FROM CART_PRODUCTS
                    WHERE NAME IN ('Milk')
                    ORDER BY CART_ID) X ON C.CART_ID = X.CART_ID
WHERE C.NAME IN ('Yogurt')
ORDER BY C.CART_ID
```
#### SELF JOIN 대신 
```sql
 #1
SELECT CART_ID
FROM CART_PRODUCTS
WHERE CART_ID IN ( SELECT CART_ID
                   FROM CART_PRODUCTS
                   WHERE NAME = '우유') AND NAME = '요거트'
ORDER BY CART_ID ASC;

#2
SELECT A.CART_ID FROM 
 (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '요거트') as A, 
 (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '우유') as B
 WHERE A.CART_ID = B.CART_ID
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
