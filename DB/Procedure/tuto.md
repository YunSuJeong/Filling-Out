# 프로시저 실습
DB툴-sqlDeveloper, 오라클 11g
  
### 🔒도전과제 : 부서코드를 입력받아 해당 부서 직원들의 월급합을 구하는 프로시저를 작성하여라
  
  
#### step1. 준비 - 데이터를 세팅해보자
부서테이블과 직원테이블을 만들어줍니다. 데이터도 넣어주세요.
```
CREATE TABLE SAMPLE_DEPT
       (DEPTNO number(10),
        DNAME VARCHAR2(14),
        LOC VARCHAR2(13) 
);

INSERT INTO SAMPLE_DEPT VALUES (10, 'ACCOUNTING', 'NEW YORK');
INSERT INTO SAMPLE_DEPT VALUES (20, 'RESEARCH',   'DALLAS');
INSERT INTO SAMPLE_DEPT VALUES (30, 'SALES',      'CHICAGO');
INSERT INTO SAMPLE_DEPT VALUES (40, 'OPERATIONS', 'BOSTON');

CREATE TABLE SAMPLE_EMP (
 EMPNO               NUMBER(4) NOT NULL,
 ENAME               VARCHAR2(10),
 JOB                 VARCHAR2(9),
 MGR                 NUMBER(4) ,
 HIREDATE            DATE,
 SAL                 NUMBER(7,2),
 COMM                NUMBER(7,2),
 DEPTNO              NUMBER(2) ,
 SUM_SAL             NUMBER(10)
 );

INSERT INTO SAMPLE_EMP VALUES (7839,'KING','PRESIDENT',NULL,TO_DATE('1981-11-17','YYYY-MM-DD'),5000,NULL,10,NULL);
INSERT INTO SAMPLE_EMP VALUES (7698,'BLAKE','MANAGER',7839,TO_DATE('1981-05-01','YYYY-MM-DD'),2850,NULL,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7782,'CLARK','MANAGER',7839,TO_DATE('1981-05-09','YYYY-MM-DD'),2450,NULL,10,NULL);
INSERT INTO SAMPLE_EMP VALUES (7566,'JONES','MANAGER',7839,TO_DATE('1981-04-01','YYYY-MM-DD'),2975,NULL,20,NULL);
INSERT INTO SAMPLE_EMP VALUES (7654,'MARTIN','SALESMAN',7698,TO_DATE('1981-09-10','YYYY-MM-DD'),1250,1400,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7499,'ALLEN','SALESMAN',7698,TO_DATE('1981-02-11','YYYY-MM-DD'),1600,300,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7844,'TURNER','SALESMAN',7698,TO_DATE('1981-08-21','YYYY-MM-DD'),1500,0,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7900,'JAMES','CLERK',7698,TO_DATE('1981-12-11','YYYY-MM-DD'),950,NULL,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7521,'WARD','SALESMAN',7698,TO_DATE('1981-02-23','YYYY-MM-DD'),1250,500,30,NULL);
INSERT INTO SAMPLE_EMP VALUES (7902,'FORD','ANALYST',7566,TO_DATE('1981-12-11','YYYY-MM-DD'),3000,NULL,20,NULL);
INSERT INTO SAMPLE_EMP VALUES (7369,'SMITH','CLERK',7902,TO_DATE('1980-12-09','YYYY-MM-DD'),800,NULL,20,NULL);
INSERT INTO SAMPLE_EMP VALUES (7788,'SCOTT','ANALYST',7566,TO_DATE('1982-12-22','YYYY-MM-DD'),3000,NULL,20,NULL);
INSERT INTO SAMPLE_EMP VALUES (7876,'ADAMS','CLERK',7788,TO_DATE('1983-01-15','YYYY-MM-DD'),1100,NULL,20,NULL);
INSERT INTO SAMPLE_EMP VALUES (7934,'MILLER','CLERK',7782,TO_DATE('1982-01-11','YYYY-MM-DD'),1300,NULL,10,NULL);
```
[출처] https://java7.tistory.com/164
  
  
#### step2. 설계 & 로직 고민
  
  
#### step3. 구현
```
create or replace procedure SAMPLE_SUM_SAL(
    in_dept_no in number
    ,out_msg out varchar2
) is
    dept_sal_sum number;
    dept_yn number;
BEGIN
    select count(1) into dept_yn from SAMPLE_DEPT where deptno = in_dept_no;

    if dept_yn <= 0 then
        out_msg := '존재하지 않는 부서입니다.';
    else
        select sum(sal) into dept_sal_sum from SAMPLE_EMP where deptno = in_dept_no;

        update SAMPLE_EMP set SUM_SAL = dept_sal_sum where deptno = in_dept_no;
        out_msg := in_dept_no || '부서의 총 월급이 계산완료되었습니다.';
    end if;
EXCEPTION when others then
    out_msg := '오류 : ' || SQLERRM;
END;

```
  
#### 결과 이미지
![프로시저_결과](https://github.com/YunSuJeong/Filling-Out/assets/91771574/4af03b4b-d6f8-4613-abf4-85e0b1d91507)
  

#### 어.? 포인트
  
