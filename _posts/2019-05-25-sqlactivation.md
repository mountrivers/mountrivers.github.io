---
title: " SQLD 핵심 정리 sql 활용 -1"
date: 2019-05-25
categories: sqld
tags: 
  - sqld
  - sql활용
---

# SQL 활용

## 순수 관계 연산자
 - 순수관계 연산자란 릴레이션의 구조와 특성을 이용하는 연산자로, 관계데이터 모델에서 제시 되었다.릴레이션에 저장되어있는 데이터를 다양하게 처리한다.
 
 - SELECT
 
 - PROJECT
 
 - JOIN
 
 - DIVIDE ( 현재는 사용되지 않음. )
 
## join 방법
 - A inner join B : A와 B가 겹치는것을 파악 한 후 겹치는 영역의 행들만 반환
 
 - A left outer join B : A기준으로 모든 행을 나열 한 후, A와 B 가 겹치는 행은 B의 데이터 추가
 
 - A right outer join B : B기준으로 모든 행을 나열 한 후, A와 B가 겹치는 행은 A의 데이터 추가
 
 - A full outer join B : A와 B의 겹치는 것을 파악 한 후 겹치는 영역의 행을 나열하고, 안겹치는 A와 B의 데이터 추가
 
## equi join 과 inner join 차이점
![innervsequijoin](https://user-images.githubusercontent.com/36880919/58365285-e5933900-7efc-11e9-83c7-da90d3f6c276.PNG)

 - equi join은 from 절에서 명시 -> where 절에 조건 / inner join 은 from 절에서 A join B ON (=using) 조건
 
## 카다시안 곱 (cartasian product)
 - 두 테이블의 모든것을 곱하여 나열한다
 
 - cross join
 
 - 로우가 늘어날수록 시간이 매우 걸림으로 거의 사용하지 않는다.
 
## using 조인과 on 조인
 - using 은 두 테이블의 칼럼 이름이 완전히 같을때 사용 ( using에 사용된 칼럼명은 테이블명.칼럼명 이 아닌 바로 칼럼명으로 호출 해야 한다.)
 
 - on은 같든 다르든 사용 가능
 
## 집합연산자의 종류
 ### 유니온
 - 유니온이란? 여러개의 sql 문을 모두 합쳐줌
 
 - 데이터 타입과 컬럼명이 같아야 한다.  ( **컬럼명은 alias로 같게 해줘도 된다.**)
 
 - union : 중복되는 데이터를 제거하고 보여줌/ union all 중복된 데이터도 다 보여줌. (그래서 union all 이 더 빠름)
 ### intersect
  - 여러 개의 sql문의 결과에 대한 교집합. 중복된 행은 하나의 행으로
  
 ### except 
 - 앞의 sql 문에서 뒤에 sql문의 결과에 대한 차집합. 중복된 행은 하나의 행으로 ( 일부에서는 minus로 사용)
 
 
 
## 계층형 질의
 - 계층형 질의란 계층으로 이루어진 데이터를 처리 하기 위해 사용
  
 ex) A 의 상사 : B, B의 상사 C 
 
 - start with : 계층 구조의 시작점을 지정하는 구문. 보통 계층의 제일 꼭대기의 상위는 null 임으로, start with 상위 is null 로 정의한다
 
 - connect by prior : 계층형으로 연결될 두개를 연결  해 준다. 자식 = 부모 or 부모 = 자식 으로 왼쪽<-오른쪽으로 정렬한다.
 부모 노드로부터 자식 노드 방향으로 전개하는 자식 = 부모 가 순방향전개이다.
 
 - order siblings 는 부모가 같은 형제 노드 사이에서 정렬 하는 것이다.
 
 - 루트 노드의 level 은 1이다.
 
 - start with 에 의해 선정된 로우는, 뒤에 connect by 에 의해 걸러지더라도 결과에 포함된다.
 
 - SQL server에서의 계층형 질의문은 CTE(common table expression)를 재귀 호출함으로써 계층 구조를 전개하며, 엥커 맴버를 실행하여 기본 결과
 집합을 만들고 이후 재귀맴버를 지속적으로 실행한다. 
 
 - 오라클의 계층형 질의문에서 where 절은 모든 전개를 진행한 이후 필터 조건으로서 조건을 만족하는 데이터만을 추출 하는데 활용된다.
  prior 키워드는 connected by, select , where 절에서 사용 할 수 있다.
  
  ## SELF JOIN
   - 동일 테이블 사이의 조인. 따라서 FROM 절에 동일 테이블이 두 번 이상 나타난다. ( = alias 를 반드시 해줘야 한다.)
   
   - 하나의 테이블에서 두 칼럼이 연관 관계가 있을 시 사용.
   
   예시 1)
   ![selfjoin](https://user-images.githubusercontent.com/36880919/58381724-aef01800-7ffb-11e9-8fec-9b55de22c18a.PNG)

  예시 2) 누적 금액 구하기

![selfjoin-1](https://user-images.githubusercontent.com/36880919/58382177-0e512680-8002-11e9-86cb-ff3cc0271932.PNG)

위와 같이 누적 금액을 구할 수 있습니다.

![selfjoin-2](https://user-images.githubusercontent.com/36880919/58382176-0e512680-8002-11e9-9f41-a0f3c4b92f60.PNG)
 
## 서브쿼리
  - 서브쿼리란 메인쿼리 내에 삽입되는 쿼리이다.
  
  - single row 서브쿼리(단일행 서브쿼리) : 서브쿼리의 실행 결과가 항상 1건 이하인 서브 쿼리. 단일행 비교 연산자로는 =,< 처럼 값 비교가 있다.(in, any, some,exists 도 사용 가능).
  
  - multi row 서브쿼리(다중 행 서브쿼리) : 서브쿼리의 실행 결과가 여러 건인 서브쿼리를 의미. 다중 행 비교 연산자인 in,any,some,exists가 있다.
  
  - multi column 서브쿼리(다중 칼럼 서브쿼리) : 서브쿼리의 실행 결과로 여러 칼럼을 반환한다. 메인쿼리의 조건절에 여러 칼럼을 동시에 비교 가능하다.
   서브와 메인쿼리에서 비교하려는 칼럼 개수와 위치가 동일해야 한다. (sql server에서는 지원 안됨)
   
  - 연관(correlated) 서브쿼리는 서브쿼리가 메인쿼리 칼럼을 포함하고 있는 형태를 말한다
  
  - 스칼라 서브쿼리 : select 절에서 함수처럼 사용되는 쿼리문. 반환 값은 한개여야 한다.
  
## 인라인 뷰 (inline view)  (=동적 뷰 dynamic view)
 - 인라인 뷰는 from 절 에 오는 서브쿼리로 view처럼 동작
 
 - 적절한 크기의 중간집합을 생성하거나 데이터 처리의 순서를 의도적으로 지정하기 위해 사용
 
 - 실행 계획의 제어를 위한 목적으로 사용 ( sql문 실행 될때만 임시적으로 생성되어 따로 저장되지 않음)

## 뷰 특징
 - 독립성 : 테이블 구조가 변경되어도 뷰를 사용하는 응용 프로그램은 변경하지 않아도 된다.
 
 - 편리성 : 복잡한 질의를 뷰로 생성함으로써 관련 질의를 단순하게 작성할 수 있다. 특히 
  자주 사용하는 sql문을 뷰로 이용하면 편리하게 사용할 수 있다.
  
 - 보안성 : 다른사람이 알면 안되는 정보가 존재하면, 뷰를 생성할 때 해당 칼럼을 빼고 생성함으로서 사용자에게 정보를 감출 수 있다.
 
 - 뷰는 정의만을 가지고 있으며, 실행 시점에 질의를 재작성하여 수행한다.
 
 - 실제 데이터를 저장하고 있는 뷰를 생성하는 기능을 지원하는 DMBS도 있다.
 
## rollup , cube, grouping sets
 - 셋다 일반 그룹 함수로 동일한 결과를 만들 수 있다.(하지만 매우 길어진다.)
 
 - rollup : 집계함수로서, 각각 합계를 나타 낼 수 있다.
 
 - cube : rollup 을 두번 한것과 결과가 같으며, 결합 가능한 모든 값에 대하여 다차원 집계를 생성한다.
 
 ex) cube (A,B) : rollup(A,B) + rollup( (A,B) )
  부하가 가장 크다.
 
 - grouping sets : 계층구조 없이, 각각에 대한 합계를 생성한다.
 
## oracle vs sql server
  - oracle 에서는 (+) 표시로 outer join 을 설정 가능함( (+) 없는쪽이 방향). sql 에서는 외부조인으로


**포스트당 너무 오래걸려서 2편으로 나누겠습니다. ㅠㅠ..**
