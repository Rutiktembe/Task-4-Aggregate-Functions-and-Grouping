# Task-4-Aggregate-Functions-and-Grouping


SQL> SELECT * 
  2  FROM EMP;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO
---------- ---------- --------- ---------- --------- ---------- ---------- ----------
      7369 SMITH      CLERK           7902 17-DEC-80        800                    20
      7499 ALLEN      SALESMAN        7698 20-FEB-81       1600        300         30
      7521 WARD       SALESMAN        7698 22-FEB-81       1250        500         30
      7566 JONES      MANAGER         7839 02-APR-81       2975                    20
      7654 MARTIN     SALESMAN        7698 28-SEP-81       1250       1400         30
      7698 BLAKE      MANAGER         7839 01-MAY-81       2850                    30
      7782 CLARK      MANAGER         7839 09-JUN-81       2450                    10
      7788 SCOTT      ANALYST         7566 19-APR-87       3000                    20
      7839 KING       PRESIDENT            17-NOV-81       5000                    10
      7844 TURNER     SALESMAN        7698 08-SEP-81       1500          0         30
      7876 ADAMS      CLERK           7788 23-MAY-87       1100                    20
      7900 JAMES      CLERK           7698 03-DEC-81        950                    30
      7902 FORD       ANALYST         7566 03-DEC-81       3000                    20
      7934 MILLER     CLERK           7782 23-JAN-82       1300                    10
SO THIS IS MY SQL TABLE AM DOING SOME AGGREAGATE OPERATIONS ON IT.

1.Apply aggregate functions on numeric columns

SQL> SELECT  MAX(SAL),MIN(SAL),SUM(SAL)
  2  FROM EMP;
  MAX(SAL)   MIN(SAL)   SUM(SAL)
---------- ---------- ----------
      5000        800      29025
      
  SQL> SELECT MAX(SAL),MIN(SAL),SUM(SAL)
  2  FROM EMP
  3  WHERE SAL>2000;
  MAX(SAL)   MIN(SAL)   SUM(SAL)
---------- ---------- ----------
      5000       2450      19275 

2.Use GROUP BY to categorize 
It Is a CLAUSE used to create the GROUP BY executing ROW BY ROW 

SQL> SELECT MAX(SAL),MIN(SAL),DEPTNO
  2  FROM EMP
  3  WHERE SAL>500
  4  GROUP BY DEPTNO;

  MAX(SAL)   MIN(SAL)     DEPTNO
---------- ---------- ----------
      2850        950         30
      3000        800         20
      5000       1300         10

      
SQL> SELECT  MAX(SAL),JOB,MIN(SAL)
  2  FROM EMP
  3  WHERE DEPTNO IN(10,20)
  4  GROUP BY JOB;

  MAX(SAL) JOB         MIN(SAL)
---------- --------- ----------
      1300 CLERK            800
      5000 PRESIDENT       5000
      2975 MANAGER         2450
      3000 ANALYST         3000

3.Filter groups using HAVING 
It Is a CLAUSE used to filter the conditions of groups 

SQL> SELECT COUNT(*),DEPTNO
  2  FROM EMP
  3  GROUP BY DEPTNO 
  4  HAVING COUNT(*)>3;

  COUNT(*)     DEPTNO
---------- ----------
         6         30
         5         20


SQL> SELECT MAX(SAL),MIN(SAL),JOB
  2  FROM EMP
  3  WHERE SAL IS NOT NULL
  4  GROUP BY JOB
  5  HAVING MAX(SAL)>1000;

  MAX(SAL)   MIN(SAL) JOB
---------- ---------- ---------
      1300        800 CLERK
      1600       1250 SALESMAN
      5000       5000 PRESIDENT
      2975       2450 MANAGER
      3000       3000 ANALYST
