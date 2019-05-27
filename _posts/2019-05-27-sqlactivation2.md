---
title: " SQLD 핵심 정리 sql 활용 -2"
date: 2019-05-25
categories: sqld
tags: 
  - sqld
  - sql활용
---

# SQL 활용 -2 

## 윈도우 함수 (Window Funciton, Analytic Function)

 - 행과 행간의 관계를 정의 하기 위해 제공되는 함수
 
 - partition 과 group by 구문은 의미적으로 유사함.
 
 - partion 구문이 없으면 전체 집합을 하나의 partition으로 정의한 것과 동일하다.
 
 - 윈도우 함수는 결과에 대한 함수처리이기 때문에 결과 건수는 줄지 않는다.
 
 - 윈도우 함수 적용 범위는 partition을 넘을 수 없다. 
 
 - over 문구가 필수 키워드로 들어감. 

- 윈도우 함수 내에서 사용한 칼럼명은 밖에서 사용 불가능

## 윈도우 함수 종류
 - RANK : 순위를 구하되, 동일한 값에 대해서는 동일한 순위를 부여한다. (ex  1 - 2 - 2 - 4)
 
 - DENSE_RANK : 순위를 구하되, 동일한 값에 대해서는 하나의 같은 건으로 순위르 ㄹ부여. ( ex 1 - 2 - 2 - 3)
 
 - ROW_NUMBER : 순위를 구하되, 동일한 값에 대해서도 순위를 따로 부여 ( ex 2가 두개여도 1 - 2 - 3 -4)
 
 - SUM, AVG, COUNT
 
 - MAX, MIN
 
 - FIRST_VALUE,LAST_VALUE : 첫값과 끝값으로 order by를 사용하기에 max,min과 동일
 
 - LAG : 이전 행 ( sql server에서 지원 X)
 
 - LEAD : 윈도우에서 특정 위치의 행의 값을 가져옴
 
 - 그 외에 CUME_DIST,PERCENT_RANK,NTITLE,RATIO_TO_RATE 등이 있다.
 
 - PRECEDING, FOLLOWING : n 만큼 앞 혹은 뒤의 행 까지의 범위
 
 
 ## DCL (data control language)
  - DBMS에 생성된 USER와 다양한 권한들 사이에서 중개 역할을 할 수 있도록 사용됨. 
  
  - grant : 유저에게 권한을 부여. 
  
  grant (기능) (부여될 유저 ) to ( 부여받을 유저)
  
  where 조건절을 사용하려면 select 권한도 줘야 한다.
  
  - revoke : 준 권한을 철회
  
  - 권한을 받은 사람은 그 권한을 다시 다른 유저에게 줄 수있다. 만약 revoke를 cascade 로 실행하면 해당 권한을 받은 사람에게 받은사람도 모두 취소된다.
  
 
 ## PL/SQL 
  - 프로그래밍 언어의 특성을 반영한 sql. (MS-SQL 에서는 T-SQL 이라고 한다.)
  
  -  블록단위 (DECLARE(선언), BEGINE, END)와 절차적 단위 ( IF,FOR,WHILE,ROOP 등) 을 사용 할 수 있다. 
  
  - 문장의 끝을 ;(세미콜론) 으로 표시 한다.
  
  - 주석 : '--' : 한줄 주석 , '/* ~ */' 여러줄 주석
  
  - 변수 할당 시 := 을 사용한다.
  
  - DMBS 정의 에러나 사용자 정의 에러를 정의하여 사용 가능
  
  - 오라클에 내장 되어 있다.
  
  - 응용프로그램의 성능을 향상
  
  - 블럭 단위로 서버와 통신이 가능하여 통신량을 줄일 수 있다.
  
  - procedure, user defined function, trigger 등 객체를 pl/sql 로 작성이 가능하다.
  
  - 객체내에서도 트랜잭션을 자율적으로 설정 할 수 있다.
  
  - procedure 내의 절차적 코드는 PL/SQL이 처리 하고, SQL문은 SQL 실행기가 처리한다.
  
  - DDL문ㅇ르 실행 할 때에는 앞에 excute immediate를 붙인다.
  
 ## triger
  - 데이터베이스에 의해서 자동으로 호출되고 수행된다.
  
  - 특정 테이블에 대하여 insert, update, delete 문이 수행되었을 때 호출되도록 정의 할 수 있다.
  
   - commit, rollback 과 같은 tcl 언어를 사용 할 수 없다.
   
   - 데이터베이스에 로그인 하는 작업에도 정의 할 수 있다.
   
   - 데이터의 무결성과 일관성을 위해서 사용자 정의 함수를 사용한다.
   
   - 테이블과 뷰, 데이터베이스 작업을 대상으로 정의할 수 있다.
   
   - 전체 트랜잭션 작업에 대해 발생되는 trigger와, 각 행에 대해서 발생되는 trigger가 있다. 
   
