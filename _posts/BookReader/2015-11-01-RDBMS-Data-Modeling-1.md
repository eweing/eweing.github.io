---
layout: post
title: RDBMS Data Modeling (1)
description: "오라클 데이터베이스 설계 & 활용 2-1장 스터디"
categories: BookReader
---

## 개념 데이터 모델링

### 개체 (Entity)
주로 하나의 테이블로 표현됨.

* 무엇을 Entity로 설정할 것인가?   
>> 관리하고자 하는 것이 무엇인가를 생각할 것.
1. 무엇을 관리할 것인가?
2. 집합의 근거가 객관적인가?
3. 집합을 이룰 수 있는가?
4. 영속적으로 존재하는 것인가?
5. 모든 Entity는 식별자(UID)를 가져야 한다.
6. 하나 이상의 명확한 속성을 포함하고 있는가?

#### Entity의 표현
* 모서리가 둥근 박스, 혹은 직사각형.   
* 이름과 속성이 들어갈 자리를 구분   
* 이름은 함축적인 명사형 단어를 선택

#### Entity의 종류
* ___Key Entity___   
최상위 Entity. 데이터를 생성하고 하위 데이터를 발생시키지만, 자신의 데이터 값은 거의 변하지 않음.
* ___Main Entity___   
Key Entity로부터 생겨난 자식 Entity지만 실제 업무의 중심 역할을 함.
* ___Action Entity___   
실제 업무 활동을 뜻하는 것으로, 가장 많은 데이터를 보유   
물품 판매, 일일 프로젝트 수행 이력 등
실제 클라이언트 측에서 발생되는 데이터가 빈번히 입/출력 및 수정 되는 Entity를 뜻함.

***

### 속성 (Attribute)
Entity를 정의하고 표현하는 속성.

* 납품 업체 Entity    
>> 납품 업체의 이름, 사업자 번호, 전화번호, 주소 등이 애트리뷰트로 선언될 수 있다.

#### Entity인가 속성인가?
__?__ 회원 테이블에서 관리자와 일반 회원은 다른 Entity로 두어야 하는가?   
__?__ 유선 전화기와 무선 전화기는 서로 다른 Entity로 두어야 하는가?

***

### 식별자 (UID)
Unique Identifier   
Entity를 대표하는 값이자 모든 데이터를 구분 지을 수 있는 식별자.   
즉, Entity의 내용들을 함축할 수 있어야 하는 대표적인 키 값.   

___Entity에서 #으로 표현___

__?__ 회원 테이블에서 회원의 id를 UID로 잡아도 되는가?

#### 두 개 이상의 UID
* 영화표 Entity를 생각해보자   
>> 영화표의 UID는 무엇으로 해야 할까?   
__?__ 상영날짜로 모든 영화표를 구분할 수 있는가?   
__?__ 상영시간으로 모든 영화표를 구분할 수 있는가?   
__?__ 좌석번호로 모든 영화표를 구분할 수 있는가?

***

### 관계 정의 (Relationships)
Relationship은 Entity간의 관계를 규정하기 위한 것으로써,
관계를 통해 UID를 상속받으며 부모와 자식간의 관계를 정립시키는 역할을 한다.

___두 Entity간의 현재의 명확한 근거나 미래의 관계를 생각하여 표현 해 주는 것___

#### 두 Entity 간의 관계 표시
일반적으로 부모에서 자식으로의 표현은, 부모에서 점선으로 출발한다.   
_>> 부모는 자식을 가질 수도, 가지지 않을 수도 있기 때문_   
부모가 있으므로 자식이 반드시 생긴다면, 실선으로 출발한다.   
그리고 받는 쪽은 삼지창 모양의 세 선으로 Many를 표현.

#### UID의 상속
부모의 UID를 자식이 상속 받는 경우는 자식 쪽에 막대기를 그려 넣어 표현.   
한 명의 사원이 하나의 부서를 갖는 것이 아니라,
한 사원이 영업부, 기획부 등 여러 개의 소속을 갖는 경우
부서별 사원이라는 Entity를 따로 만들었다고 했을 때,
부서별 사원 Entity는 부서의 UID와 사원의 UID를 상속 받아야 함

#### 관계명칭 표현과 M:1
가장 일반적인 관계. 자식 : 부모의 관계이다.   
운동선수와 프로팀의 관계로 예를 든다면 프로팀이 존재해야 그 팀의 소속선수가 있는 것과 같다.   
양방향을 왼쪽에서 오른쪽, 오른쪽에서 왼쪽으로 차례대로 표현.   
관계명칭은 대체로 부사나 형용사로 표현 해 주는 것이 의미상 해석하기 좋음.

#### M:M과 1:1 관계
* M:M 관계   
의사와 환자의 경우, 환자는 여러 의사에게 진료를 받을 수 있고, 의사는 여러 환자를 진료할 수 있다.
* 1:1 관계   
침대 하나에 매트리스 하나가 들어갈 수 있다. 이 경우 1:1   
하지만, 침대에 넣을 수 있는 매트리스 교체 이력을 생각한다면 1:M 관계가 된다.   
1:1로 생각되었다가 하나의 Entity로 통합되는 경우가 굉장히 많음.   
따라서 1:1관계가 존재하더라도 상속의 개념 보다는 의미상 표현에 가까울 수 있다.
