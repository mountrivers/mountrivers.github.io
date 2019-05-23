---
title: " SQLD 핵심 정리 DCL, DML 실전 사용해보기 "
date: 2019-05-20
categories: sqld
tags: 
  - sqld
  - sql기본
  - ddl
  - dml
---

## 데이타 베이스 만들기
![database](https://user-images.githubusercontent.com/36880919/58261074-99d47880-7db2-11e9-84cc-c62f571f0e56.PNG)

create database [데이타베이스이름];

use [데이타베이스이름];


## 테이블 만들기와 자료 넣기
![maketable](https://user-images.githubusercontent.com/36880919/58261298-fe8fd300-7db2-11e9-8a96-a4f0702003a9.PNG)

테이블 생성 : create table [테이블이름] ( 칼럼이름 칼럼자료형, --- ) ;

테이블에 값 추가 : insert into 테이블명(칼럼이름 ,--)value(추가할값);

테이블 값 확인 : select * from [테이블이름]

## 테이블에서 특정 값 삭제하기
![delete](https://user-images.githubusercontent.com/36880919/58261434-46165f00-7db3-11e9-86da-f168f5088819.PNG)

delete from [테이블명] where 칼럼명 = 조건


## 테이블 이름 바꾸기
![rename](https://user-images.githubusercontent.com/36880919/58261461-529ab780-7db3-11e9-90eb-1a2fcc50d4cc.PNG)

rename table [테이블명] to [바꿀테이블명];

## 테이블 칼럼 추가하기
![alter add](https://user-images.githubusercontent.com/36880919/58261460-52022100-7db3-11e9-9654-96dda4cd5c9c.PNG)

alter table [테이블명] add [칼럼명] [칼럼자료형];

## 테이블 칼럼 자료형 변경하기
![alter modify](https://user-images.githubusercontent.com/36880919/58261459-52022100-7db3-11e9-9266-53f180414a9e.PNG)

alter table [테이블명] modify [칼럼명] [바꿀 칼럼자료형];

## 테이블 칼럼 이름 바꾸기
![alter change](https://user-images.githubusercontent.com/36880919/58261457-52022100-7db3-11e9-9abf-effc65727c2d.PNG)

alter table [테이블명] change [칼럼명] [바꿀 칼럼명] [바꿀 칼럼자료형];

## 테이블 칼럼 삭제하기
![alter drop](https://user-images.githubusercontent.com/36880919/58261456-51698a80-7db3-11e9-83ab-8e3e5fff81d2.PNG)

alter table [테이블명] drop [칼럼명];

## 테이블 삭제하기
![drop](https://user-images.githubusercontent.com/36880919/58261454-50d0f400-7db3-11e9-8a51-794c0da1911c.PNG)

drop table [테이블명];

## 테이블 자료 조회, 검색
![select1](https://user-images.githubusercontent.com/36880919/58261453-50d0f400-7db3-11e9-99fa-7de8fe391017.PNG)

select [칼럼명] from [테이블명];

여기서 칼럼명에 *을 넣으면 모든 칼럼을 다 보여주게 됩니다.

특정 데이터 검색
where + 조건

![select2](https://user-images.githubusercontent.com/36880919/58261452-50385d80-7db3-11e9-9d55-0b584536ff85.PNG)

검색시 and 나 or 을 사용하여 두개 이상의 조건으로 검색 할 수 있으며,

where [칼럼명] like '%x%' 형식으로 특정 글자를 포함하는 것을 검색 할 수 있습니다.

like 뒤에

**'%A'** 는 ~~A 처럼 뒤가 A로 끝나는 것을 검색 해 줍니다.

**'A%'** 는 A~~ 처럼 맨 앞이 A로 시작하는 것을 검색 해 줍니다.

**'%A%'** 는 ~ A~ 처럼 어느 위치든 A가 들어가는 것을 검색 해 줍니다.

## 기본키 설정
![pk1](https://user-images.githubusercontent.com/36880919/58261470-53cbe480-7db3-11e9-80b8-b42ff56ef3a6.PNG)

![pk2](https://user-images.githubusercontent.com/36880919/58261469-53cbe480-7db3-11e9-8721-f466d6ddcefa.PNG)

table 을 만들 때 

맨 아래에 primary key (칼럼명); 이나 

constraint [제약조건이름] primary key(칼럼명) 

식으로 기본키를 설정 할 수 있습니다.

## 2개 이상을 묶어서 기본키로 설정
![pk3](https://user-images.githubusercontent.com/36880919/58261466-53334e00-7db3-11e9-99bf-b8a04db45ba5.PNG)

칼럼명을 여러개 써주면 묶어서 기본키로 설정 해 줍니다.

## 이미 생성한 테이블에 기본키 설정하거나 삭제 하기
![pk5](https://user-images.githubusercontent.com/36880919/58261463-529ab780-7db3-11e9-901b-d9651c43859b.PNG)

기본키 설정 : alter table [테이블명] add constraint pri_key primary key (칼럼명);

기본키 제거 :  alter table [테이블명] drop primary key;

## 제약사항들 확인하기
![constraint1](https://user-images.githubusercontent.com/36880919/58261462-529ab780-7db3-11e9-9f56-d80162c40848.PNG)

desc [테이블명];



**임시 저장 상태입니다. 뒤에 제약사항에 대해서만 조금 이어가고 나머지는 이론 정리하며 풀어나가겠습니다.**
