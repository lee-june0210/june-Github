# Database


### SQL 문법 정리

SELECT * FROM  DEPARTMENT;
select empno, name, job from employee;
SELECT concat( empno, '-', deptno) AS '사번-부서번호' 
FROM employee;
select distinct deptno from employee;
select empno, name, job from employee order by name;

select empno as 사번, name as 이름, job as 직업 from employee order by 이름;
select empno, name, job from employee order by name desc;
