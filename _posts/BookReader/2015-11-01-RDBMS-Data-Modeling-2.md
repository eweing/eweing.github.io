---
layout: post
title: RDBMS Data Modeling (2)
description: "오라클 데이터베이스 설계 & 활용 2-3장 스터디"
categories: BookReader
---

## 상세 개념 데이터 모델링
기본적으로는 Entity, 속성, 관계를 바탕으로 표현하는 것이지만,
기본 개념 데이터 모델보다 어려울 수 있음.

***

### 기본키 (Primary Key)
UID가 상세 개념으로 넘어오면서 PK로 변한다.

#### PK의 특징
1. 테이블에 한개 또는 그 이상 존재한다.
2. 테이블의 모든 데이터를 Unique하게 만들어준다.   
즉 PK를 통해 각 ROW를 구분할 수 있다.
3. 모든 테이블에는 반드시 PK가 존재한다.
4. NOT NULL

#### 상속받는 PK
PK는 자식 Entity에 상속 가능.    
이 경우 자식 Entity에는 속성명을 적지 않는다.

***

### 외부키 (Foreign Key)
관계에서 상속받는 UID가 현재 테이블의 FK가 되는 경우 사용.   
PK로 상속 받는 것과 차이가 있다. 단순히 두 테이블 간의 관계를 성립하기 위해 사용하는 것.   
상속받은 자신은 따로 PK가 존재한다.

***

### 정규화 (Normalizing, Normalization)
* __제 1정규형__   
_모든 Attribute는 원자값을 갖는다. 반복 형태가 있어서는 안된다._
* __제 2정규형__   
_모든 Attribute는 반드시 UID에 종속되어야 한다._   
만약 UID 일부에 종속된다면, 해당 Attribute는 다른 테이블로 옮겨져야 한다.   
제 2정규형을 따름으로써 부모 자식 관계로 종속되어 있는 테이블의 속성값은
입력, 수정시 불필요한 데이터 입력량을 줄일 수 있다.
* __제 3정규형__   
_UID가 아닌 Attribute사이에는 서로 종속될 수 없다._   
다음과 같은 경우에 하는 것이 좋다.   
>> 또 다른 자식 Entity가 생겨날 때   
>> 서브타입의 하위속성이 계속 추가될 때   
>> 다른 Entity에서도 관계를 갖게될 때

#### 제 1 정규형
환자와 진료기록

#### 제 2 정규형
주문 내역 Entity에서 물품 정보와 배송 정보를 다른 Entity로 빼내기

#### 제 3 정규형

***

### M:M? 1:M!
대다수의 데이터는 M:M 관계이지만, DB에 저장하고 효율적으로 관리하기 위해서는 1:M 관계로 풀어내야 한다.   
환자와 의사의 경우, 직접적으로 연결하면 M:M 관계지만,   
그 사이에 진료목록 Entity를 넣으면 의사-진료목록, 진료목록-환자 간에 1:M 관계를 만들 수 있다.

***

### 순환관계
자기자신을 참조하는 경우.   
순환관계의 가장 대표적인 예는 바로 게시판이다.   
게시판에서는 자신의 글 밑에 다른 사람들의 댓글이 달리는 구조.   
그 외에도 '회사 > 공장 > 부서 > 팀' 처럼 조직 Entity를 순환 관계 설정하는 경우도 있다.   
1:M 혹은 1:1 관계로 표현

***

### BOM
Bill of Material (자재명세서)   
제품 하나가 어떤 부품들로 이루어져 있는가에 대한 데이터.   
M:M 순환관계를 풀어낼 때 주로 사용.

#### 부품 Entity로 알아보는 BOM
제품은 여러 부품으로 구성되고 또 하나의 부품도 여러 부품으로 구성된다.   
이 경우 부품과 부품은 M:M 관계를 맺음.   
이러한 M:M 순환관계의 모델을 교차 Entity 생성으로 해결할 수 있다.   

***

### 시계열관리 (이력관리)
이력관리를 위해서는 일반적으로 이력 관리용 Entity를 생성하는 것이 원칙.   
하지만 자신의 Entity 자체가 이력이 되는 경우도 있음.

#### 이력관리 모델 선정시 고려 해야 하는 것
1. 과거 데이터의 쓰임새
2. 검색 유무
3. 입력 후 수정이나 삭제와 같은 이벤트 관리가 필요한지
4. 시간이 지난 후 모델간 관계가 변할 수 있는지

#### Entity 형태
1. 교차 Entity
2. Attribute를 분리하여 Entity로 변환

***

### 배터적 관계와 데이터 통합
Entity를 선정하고 모델링 하는 과정에서
특정 Entity가 다른 두 개 이상의 Entity 모두와 관계를 가지는 경우 있음.
이러한 경우를 배타적 관계라고 한다.   
___서로 다른 두 개의 Entity를 가지고 합집합을 이루지만 둘 중 하나를 선택해야 하는 경우___   

#### 배타적 관계가 발생하는 이유?
모델링을 하면서 Entity 자체를 명확하게 구분짓지 못하기 때문.   

#### 배타적 관계가 발생했을 경우?
__? Entity 통합을 할 것인가?__   
>> Entity의 융통성이 좋아지지만, Entity의 의미 자체가 모호해 질 수 있다.   
__? 현재 의미 그대로 둘 것인가?__   
>> 의미는 분명해지지만, 유사한 Entity가 추가되고
새로운 프로세스가 추가될 때 또 다른 배타적 관계가 생성될 수 있다.

#### 배타적 관계 표현
일반적으로 Arc(호)로 표현.   
아크는 하나의 Entity에 속해야 함.
하나의 Entity에 다수의 아크가 사용될 수 있어도, 다른 Entity의 아크와 겹쳐질 수는 없다.

\ | 장점 | 단점
------------ | ------------- | ------------
통합 | 데이터 액세스가 간편                 | 테이블 컬럼 수 증가
    | 수행 속도가 좋아질 수 있음.           | 테이블 블록 수가 증가
    | 복잡한 처리를 하나의 SQL로 통합 가능.   | 인덱스 크기가 증가
분할 | 처리시마다 SubType 유형 구분이 불필요  | 트랜잭션 처리시 여러 테이블을 처리
    | 전체 테이블 스캔시 유리              | UID 유지 관리가 어려움
    | 단위 테이블의 크기가 감소             | 복잡한 처리의 SQL 통합이 어려움

***

### 반정규화 (Denormalizing, Denormalization)
정규화 과정을 거치는 것이 모델링의 기본 조건이지만,
정규화를 모두 충족시켰을 때 수행 속도가 떨어질 수 있다.   
이 때 선택적으로 테이블을 재분할 할 것인지 중복 테이블과 컬럼을 생성시킬 것인지를 고려하고
테이블을 제거하는 경우 또한 고려해야 한다.   
즉, 선택적으로 반정규화를 통해 이러한 문제들을 해결 한다는 것.

#### 반정규화 예시
1. 테이블 통합
    * SubType을 SuperType으로 통합
    * 1:1 관계를 하나의 Entity로 통합
    * 1:M 관계의 통합
2. 테이블 분할
    * 수직, 수평 분할
3. 테이블 추가
    * 중복 테이블
    * 이력 테이블
    * 통계(연산) 테이블
    