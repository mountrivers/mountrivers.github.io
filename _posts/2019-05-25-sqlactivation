---
title: " SQLD 핵심 정리 sql 활용"
date: 2019-05-20
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
 
 
 **현재 임시저장 상태입니다.**
 
 
 ## oracle vs sql server
  - oracle 에서는 (+) 표시로 outer join 을 설정 가능함( (+) 없는쪽이 방향). sql 에서는 외부조인으로
