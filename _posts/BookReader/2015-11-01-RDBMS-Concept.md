---
layout: post
title: RDBMS Concept
description: "오라클 데이터베이스 설계 & 활용 1장 스터디"
categories: BookReader
---

## RDBMS의 정의와 종류

### RDBMS
Relational Database Management system

### 계층형 모델
* 데이터 레코드들을 계층 구조로 표현
* 계속해서 자식을 형성해 나가는 구조.
* 다른 레코드에 대한 포인터를 가지고 가리키는 구조

### 네트워크형 모델
* 데이터베이스가 레코드 타입과 링크로 구성되어 있음
* 자식 레코드가 부모 레코드를 가리키는 포인터를 가질 수 있음

### RDB (Relational Database)
각각의 테이블에 데이터를 집어 넣고   
상호관계에 따라 데이터를 결합함으로써 유용한 정보를 창출   
하지만, 각각의 시스템 환경과 작업 규모에 따라서 DBMS 선택을 고려해야 한다.

### RDB 이론
* 데이터베이스 시스템은 사용자에게 제공되는 논리적 관점과,
데이터베이스가 저장되는 물리적 구조가 확연히 구별 되어야 한다.
* 데이터는 테이블 폼 안에서 보여져야 한다.
* 하나의 테이블 안에서 구성된 n개의 속성은 관계를 구성한다.
* 각 테이블은 하나 이상의 테이블에 키가 되는 컬럼을 갖고 있다.   
그 키에 포함된 속성들은 각 관계를 식별한다.
* 데이터베이스에 접근할 수 있도록 고안된 상위레벨의 언어를 제공한다.
* 공통컬럼을 가진 테이블끼리 JOIN 연산이 가능해야 한다.
* 관계연산을 이용하여 수학적으로 정의된 연산이 가능해야 한다.

***

## Database의 역할

### MIS (Management Information System)
경영 정보 시스템

* CRM (Customer Relationship Management) 고객 관계 관리
* ERP (Enterprise Resource Planning) 전사적 자원관리
* SCM (Supply Chain Management) 공급망 관리

다양한 부분에서 핵심 시스템으로 사용됨

***

## 정리
다양한 Management System에서 사용되고 있는 데이터베이스   
단순히 정보를 쌓는 역할만 하지말고, 이를 체계적으로 관리하고 분석한다면   
그 속에서 새로운 핵심 정보를 찾아낼 수 있다.
