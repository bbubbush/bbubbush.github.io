---
layout: post
title: <그림으로 공부하는 오라클구조> Chapter2. 오라클의 여러 프로세스
category: Book_Review
categories: [Book_Review]
author: bbubbush

comments: true
---

주말은 왜이리 짧게 느껴지는지 모르겠다. 3일을 쉬어도 짧고, 2일을 쉬어도 짧고... 연금복권에 당첨되면 좋겠다.

이번주도 우선 2장에 대한 결론을 먼저 내리고 시작하겠다.

# 오라클은 병렬처리와 응답에 대해 깊은 고민을 하여 만든 소프트웨어이다!

![필기내용](/assets/img/book_review/01_oracle_architecture/2019-03-03_oracle_01.jpg){: .center .img}

일반적인 어플리케이션은 서로간의 데이터에 침범하지 않는다. 예를들어 그림판과 계산기를 열어 계산기에 입력한 값을 그림판에 찍히게 할 수는 없다. 반대로 그림판에 숫자를 중학교 수학선생님처럼 바르게 그려도 계산기에 숫자가 입력되지 않는다.  

이는 서로 다른 어플리케이션이 각자의 데이터에 접근하지 못하기 때문이다.(개발자가 의도적으로 독립적인 구조로 만들었을 수도 있다)

반면 데이터베이스는 이들과는 다르다. SQL Developer로 접속하나, JDBC 드라이버로 접속하나, CMD에 SQL Plus를 입력해서 접근하나 모두 동일한 데이터를 갖게 된다.  

**여러사용자나 프로그램이 데이터베이스의 데이터를 공유하고 있다** 이것이 데이터베이스가 여타 어플리케이션과 구분되는 가장 큰 차이점이다. 

### 서버프로세스와 백그라운드 프로세스
오라클은 여러 프로세스로 구성되어 있는데 이를 주요 업무에 따라 둘로 구분하면 서버프로세스와 백그라운드 프로세스로 구분할 수 있다.  

서버프로세스는 SQL문을 담당해서 처리하고 백그라운드 프로세스는 서버프로세스를 돕는 역할을 담당한다.  
예를들어 쿼리를 작성하고 있는 나는 서버프로세스이고 내 개발일정을 확인해주는 개인비서님과 출퇴근 길을 편하게 모시기 위해 준비하고 있는 운전기사님 내가 업무를 잘 할 수 있도록 지원하시니 백그라운드 프로세스라고 할 수 있다.(오늘도 로또를 사러간다)  

백그라운드 프로세스는 각자의 역할(role)에 따라 다시 여러 프로세스로 구분된다. 아래는 백그라운드 프로세스 중 대표적인 아이들과 그들이 하는 역할이다.

- ora_dbwX_XXXXXX : '데이터베이스 라이터'라고 읽으며, 데이터를 디스크에 기록한다
- ora_lgwr_XXXXXX : '로그 라이터'라고 읽으며 로그를 디스크에 기록한다
- ora_pmon_XXXXXX : '피몬'이라고 읽으며 프로세스를 감시하고 장애가 발생하면 이를 정리한다
- ora_arcX_XXXXXX : '아카이버'라고 읽으며 로그데이터를 아카이브한다.

이처럼 백그라운드는 다양한 일을 처리하며 서버프로세스를 돕는다. 그럼 서버프로세스는 이런 힘든 일을 다 안하면서 꿀만 빠는걸까?

천만에 말씀이다. 각 클라이언트에서 요청하는 쿼리를 상대하는 것은 마치 '영업담당자'와 같은 일을 한다. 실제로 쿼리를 보내는 것도 고객(클라이언트)이니까!

아래 그림은 오라클의 요청과 응답을 간단하게 그림으로 표현한 것이다.

![오라클의 간략구조](/assets/img/book_review/01_oracle_architecture/2019-03-03_oracle_02.jpg){: .center .img}

이 책은 위의 그림처럼 오라클이 동작하는 모습을 이미지화 하길 바란다. 이런 능력이 현장에서 오라클 엔지니어에게 큰 힘이 된다고 믿기 때문이다.  

나 역시 이런 구조를 이미지화 시키든, 텍스트화 시키든 개개인에 맞게 파악하고 있어야 한다 생각한다.  이는 생각보다 어려운 일이고, 생각보다 큰 힘이 되어준다.

이번 장에서는 오라클이 다른 어플리케션과 다른 차이점과 프로세스별 역할에 대해 정리했다. 이 내용을 각자의 방법으로 머리속에 잘 정리하길 바란다.(기억의 궁전이 있다면 방 어디 하나쯤 열어서 담아두길 바란다 ㅎㅎ )

##### 긴 글을 읽어주셔서 감사합니다 : )