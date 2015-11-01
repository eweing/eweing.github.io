---
layout: post
title: SQL Injection
description: "SQL 인젝션 공격 방법에 대해 공부해 본다."
categories: Study
---

## SQL 삽입 공격
응용 프로그램의 보안 상 허점을 의도적으로 이용해, 개발자가 생각하지 못한 SQL문을 실행되게 함으로써 데이터베이스를 비정상적으로 조작하는 공격 방법

1. 접근 제어를 우회할 수 있음
2. 일반적인 인증과 인증 확인을 무시한 채 OS 단계 명령을 수행
3. DB 내부의 데이터를 뽑아낼 수 있음

개발자가 쓴 쿼리의 나머지 부분을 무시하고 공격자의 쿼리만을 실행할 수 있게 하기 위해 - - (SQL문법상 주석 처리) 를 붙인다.

***

#### 예시 - 01. 로그인 (PHP)
{% highlight php %}
<? php
    $result = mysql_query("SELECT * FROM member WHERE ID='$id' AND PW='$pw'");
    if (mysql_num_rows($result)) {
      // 로그인 성공
    } else {
      // 사용자의 아이디와 비밀번호가 틀리므로 로그인 실패
    }
?>
{% endhighlight %}
일반적인 경우 이 로직은 정상적으로 로그인 기능을 수행한다.

하지만 여기서 $id에 ' OR '1'='1' --' 와 같은 값이 들어가게 되면 SQL 쿼리문은 다음과 같이 된다.

{% highlight SQL %}
SELECT * FROM member WHERE ID=' OR '1'='1' -- ' AND PW='$pw'
{% endhighlight %}
ID 내부에 있는 - - 값으로 인해 이후가 주석처리되고 반드시 로그인 되는 현상이 발생한다.

***

#### 예시 - 02. 글과 패스워드 출력 (PHP)
다음과 같은 쿼리가 존재할 때
{% highlight php %}
<?php
    $query  = "SELECT id, name, inserted, size FROM products
               WHERE size = '$size'
               ORDER BY $order LIMIT $limit, $offset;";
    $result = odbc_exec($conn, $query);
?>
{% endhighlight %}

아래와 같은 질의를 입력함으로써 글과 패스워드를 모두 출력할 수 있다.
{% highlight SQL %}
'
union select '1', concat(uname||'-'||passwd) as name, '1971-01-01', '0' from usertable;
--
{% endhighlight %}

***

#### 해결방법
이를 해결하는 방법은 다음과 같이 $id 와 $pw 같이 입력 받는 값을 변수에 넣어 유효성 검사를 진행하거나 SQL에 맞게 인코딩 하면 된다.

{% highlight php %}
<? php
    $id = mysql_real_escape_string($id);
    $pw = mysql_real_escape_string($pw);
    $result = mysql_query("SELECT * FROM member WHERE ID='$id' AND PW='$pw'");

    if (mysql_num_rows($result)) {
      // 로그인 성공.
    } else {
      // 사용자의 아이디와 비밀번호가 틀리므로 로그인 실패
    }
?>
{% endhighlight %}

***

### 정리
SQL Injection은 입력 필드에 SQL문을 입력함으로써
기존의 쿼리를 무시하고 공격자가 의도하는 쿼리를 수행해
데이터베이스를 비정상적으로 조작하는 공격이다.

이러한 공격을 막기 위해서는
입력받은 값의 자료형을 검사하거나, SQL 인코딩을 통해 올바른 값이 들어가도록 처리 해야 한다.

JDBC MySQL의 경우 Statement 문을 사용하면 입력받은 값을 sql문에 연결하여 하나의 SQL문으로 만든 뒤 query 를 실행하는데,
이 경우 SQL Injection 공격에 피해를 받기 쉽다.

따라서 sql문에 연결 하기 전 반드시 자료형 검사를 하거나, PreparedStatement 문을 사용하여 데이터 타입에 맞춰 값을 설정할 수 있도록 처리해야 하겠다.
