![image](https://github.com/user-attachments/assets/8d25c2fb-3dfd-49b2-b634-365662ca6b4b)# SQLD 자격증 보수교육 정리
> 보수교육링크 : https://www.dataq.or.kr/www/mypage/reedu/list.do

## 데이터 모델링의 이해
- 정의
  - 데이터 베이스 시스템이나 정보시스템에서 데이터 구조를 체계적으로 정의하고 설계하는 과정
  - 조직의 정보 수집과 관리 시스템을 정의하는 시각적 표현 또는 청사진을 생성하는 프로세스
- 중요성
  - 다양한 이해관계자들의 커뮤니케이션을 촉진하고 조직의 데이터에 대한 통일된 개념을 생성
  - 데이터 모델을 통해 sw개발 개발 생산성 및 효율성 증진, 오류 감소
  - 조직이 관리하는 데이터 문서화, 전사 시스템 설계의 일관성을 조정
- 단계
![모델링 단계](https://github.com/user-attachments/assets/3bef4d02-df8a-4fd2-a8db-d6b916b0d458)

### ▶︎ 데이터 모델링의 3요소
![3요소](https://github.com/user-attachments/assets/292bd13b-0f61-4af8-9618-a7df9d72d16c)

### 데이터 모델링 
**엔터티(Entity)**
> ∙ 업무에 필요하고 유용한 정보를 저장하고 관리하기 위한 집합적인 것(Thing)  
> ∙ 업무 활동상 지속적으로 관심을 가지고 있어야하는 대상으로서 그 대상들 간에 동질성을 지닌 인스턴스들이나 그들이 행하는 행위의 집합
- 엔터티의 요건
  - 업무에서 필요로하는 정보
  - 인스턴스(레코드)는 유일하게 각각 식별가능해야함
  - 2개 이상의 인스턴스 집합이어야함
  - 업무 프로세스에 의해 이용되어야함(다른 엔터티와 관계 혹은 프로세스 상의 관계를 가지고 있는지 점검)
  - 속성을 포함해야함
- 엔터티의 명명과 설명  
  `⚠️ 엔터티명과 설명은 데이터를 오해없이 정의하고 사용할 때 매우 중요하며, 따라서 모델링 지침서나 가이드에 반드시 포함되어야함.`
  ![원칙](https://github.com/user-attachments/assets/8e6cbda6-b3c0-4e27-91f3-6776da64318e)

**속성(Attribute)**
> ∙ 엔티티의 정보를 구성하는 의미상 더 이상 분리할 수 없는 최소의 데이터 단위
- 구성요소
  - 속성명(Name) : 속성의 내용이나 목적이 무엇인지 알려주는 명사/명사구
  - 도메인(Domain) : 속성이 지닐 수 있는 값에 대한 업무적인 제약조건, (데이터타입+길이) 적용된 개념
  - 선택성(Nullable) : 모든 인스턴스의 해당 속성이 반드시 값을 가져야 하는지에 대한 여부
- 표준화
  - 용어사전을 이용하여 표준화하는 것을 권장
  - 표준용어는 표준단어로 구성되며, 표준도메인을 속성으로 갖는다

**관계(Relationship)**
> ∙ 엔터티의 인스턴스 사이의 논리적인 연관성으로서 존재의 형태/행위로서 서로에게 연관성이 부여된 상태
> ∙ 2개의 엔터티 사이에 나타나며, 존재에 의한 관계와 행위에 의한 관계로 분류할 수 있음
- 관계의 표기법
  - 관계차수(Cardinality), 관계선택사양(Optionality), 관계명 & 식별자관계 여부
![표기법](https://github.com/user-attachments/assets/d86d3840-7707-4622-b8c6-fc7848fc93ac)

**식별자(Identifier)**
> ∙ 엔터티에서 인스턴스 각각을 구분할 수 있는 논리적인 이름
> ∙ 엔터티에 구성된 여러 개의 속성 중에 엔터티를 대표할 수 있는 속성(들)
- 구성 요건
![구성요건](https://github.com/user-attachments/assets/b2b753cd-823d-472f-aa55-b00631a4c904)
- 주식별자 도출 기준
  - 해당 업무에서 자주 조건으로 이용되는 속성
  - 명칭, 내용 등 이름으로 기술되는 것은 피하기
  - 주식별자 속성의 수가 너무 많아지지 않도록 하기
- 식별자 종류
  - Natural Key : 키 역할을 하는 데이터베이스 객체의 기존 특성 값
  - Artificial Key : 자동으로 생성되며 고유한(본질적인) 의미가 없지만 데이터베이스 사용자에게 작업에서 중요
  - Surrogate Key : 데이터베이스 개발자가 특정 설계 목적으로 생성하며 사무직 직원과 데이터베이스 사용자에게는 의미가 없고 사용하지 않음
  
> 식별자 선정은 집합을 정의하는 KEY인 동시에 데이터 정합성, 데이터 성능에도 많은 영향을 미침  
> 따라서 필요에 따라 적정한 식별자 단절 전략을 사용해야함

### 정규화(Normalization)
`E.F.Codd의 관계형 데이터베이스 이론은 데이터를 테이블로 구성하고 데이터의 중복을 최소화하여 데이터의 무결성을 유지하는 것이 핵심`
> 이상 현상(Anormaly)을 야기하는 속성 간의 종속 관계를 제거하기 위해 엔터티를 작은 여러 엔터티로 무손실 분해하는 과정
- 목적
  - (불필요한 데이터 중복을 제거하여)**데이터 조작 시 발생하는 이상 현상 제거** → 공간 절약, 무결성 확보
  - 데이터베이스 구조 확장 시 재셜계 필요성 최소화
  - 사용자에게 데이터 모델을 더욱 의미있게 만들기
  - 다양한 질의 지원
  - 테이블 구성을 논리적이고 직관적으로 변경하며, "관리해야 할 대상 데이터"를 발견
- 정규형(Normal Form)
  ![정규형](https://github.com/user-attachments/assets/80677436-20d8-4d5e-a0a1-2886aba63769)


## 데이터 모델과 SQL
### Null 속성의 이해
> Null과의 연산은 항상 Null임

![image](https://github.com/user-attachments/assets/caae0b01-d007-4394-8b62-1d5546b72bd6)
> 집계 함수는 Null값을 제외하고 처리한다.

![image](https://github.com/user-attachments/assets/edae92ad-2a54-4c62-8b75-da6daa2bce60)
> COUNT와 SUM 사용 시 주의할 사항, 고려할 사항

![image](https://github.com/user-attachments/assets/8c61d0ba-f313-4bc8-865e-0cc8e77b4633)

--- 
## SQL 기본
### 데이터 집합 연산
- 일반 집합 연산자
  - Union : UNION/UNION ALL, 합집합
  - Intersection : INTERSECT, 교집합 
  - Difference : EXCEPT(MINUS)
  - Product(Cartesian Product) : CROSS JOIN
- 순수 관계 연산자 (관계형 데이터베이스를 구현한기 위해 새롭게 만들어진 연산자)
  - Select : WHERE절로 구현
  - Project : SELECT절 컬럼 선택으로 구현
  - (Natural) JOIN : 다양한 JOIN으로 구현
  - Divide : 사용되지 않음
 
### SELECT 문의 실행 순서
> 어떻게 쿼리문을 작성하느냐에 따라 퍼포먼스 차이 발생!
1. FROM절 - 집합을 가져옴
2. WHERE절 - 조건에 맞는 데이터만 ACCESS / FILTERING
3. GROUP BY절 - 추려진 집합을 GROUPING
4. HAVING절 - GROUPING된 결과를 조건에 따라 FILTERING
5. SELECT절 - 어떤 열을 어떻게 출력할지 결정
6. ORDER BY절 - 데이터 정렬
![image](https://github.com/user-attachments/assets/ccc3e777-13f0-4478-9767-0c3c613a2f96)
- 제약사항
  - ALIAS 사용 여부 : ORDER BY절에선 사용가능, WHERE 또는 HAVING 사용 불가능함
  - ORDER가 적용된 순서를 출력하고 싶다면 SELECT절을 감싼 뒤 ROWNUM을 써야함
- 고려사항 : 성능을 위해 가급적 조건은 WHERE절에서 처리할 것

### 조인(JOIN)
> JOIN은 두 개 이상의 테이블들을 연결해 데이터를 출력하는 데이터베이스의 연산  
> 조인 조건을 만족하지 않더라도 해당 행을 반환하는 JOIN방식을 OUTER 조인  
> 해당행을 반환하는 집합을 OUTER집합이라고 함

<img src="https://github.com/user-attachments/assets/f36d63ef-d5ff-4706-848c-98610d084d14" width="350" height="200"/><br>
<img src="https://github.com/user-attachments/assets/9d110423-e89f-4508-b9d1-d06420234475" width="300" height="450"/>

- ANSI 조인 vs ORACLE 조인 (ORACLE방식의 문제점)
  - 조인 조건과 WHERE 조건의 구분이 불명확함
  - IN, OR, BETWEEN, LIKE 연산자 사용 시 에러 발생 (ORA-01719)
  - (+)표시가 누락된 조인 및 검색 조건 존재 시 OUTER가 아닌 INNER로 동작함
  - FULL OUTER JOIN을 지원하지 않음
  - 다른 DBMS로 프로그램의 이식할 때 SQL 변경 비용 발생
  
## SQL 활용
### 서브쿼리
> 서브쿼리는 SQL문 안에 포함되어 있는 또 다른 SQL

<img src="https://github.com/user-attachments/assets/9ff419b4-6439-4942-bc60-1ff147f6c4b6" width="400" height="300"/>

- 서브 쿼리는 괄호로 감싸서 기술
- 서브 쿼리는 단일 행 또는 복수 행 비교 연산자와 함께 사용할 수 있음
  - 단일 행 비교 연산자는 서브 쿼리의 결과가 반드시 1건 이하
  - 단일 행 비교 연산자 : =, <, <=, >, >=, <>
  - 다중 행 비교 연산자 : IN, ALL, ANY(=SOME), EXISTS
- 서브 쿼리 사용 가능 위치
  - SELECT절, FROM절, WHERE절, HAVING절
  - ORDER BY절, INSERT문의 VALUES절, UPDATE문의 SET
- 스칼라 서브 쿼리 : 컬럼을 쓸 수 있는 대부분의 곳에서 사용할 수 있는 서브쿼리
  - 한 행, 한 컬럼만 반환하는 서브 쿼리
  - 메인 쿼리의 결과 건수만큼 반복수행 되므로 사용 시 주의 필요
- EXISTS 서브 쿼리는 항상 Correlated(연관) 서브 쿼리로 사용 (연관 서브 쿼리로 작성하지 않아도 문법상 오류가 나지는 않음)  
  `※ EXISTS절은 조건에 해당하는 ROW의 존재 유무 체크 후 더 이상 수행하지 않는다. 일반적으로 IN에 비해 성능이 좋음`

### 서브 쿼리와 성능
> 스칼라 서브쿼리는 메인 쿼리의 결과에 대해 LOOP방식으로 동작하기 때문에 사용상 주의가 필요하지만, 특정한 조건에서는 좋은 성능을 보여줌

## 관리 구문
