---
layout: post
title: "[Spring] 동적 쿼리 처리를 위한 Querydsl 설정"
subtitle: Spring
date: '2023-03-21 10:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Querydsl`을 사용하기 위한 설정을 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
JPA의 쿼리 메소드 기능과 @Query를 통해 많은 기능을 구현할 수 있지만, 선언할 때 고정된 형태의 값을 가진다는 단점이 존재합니다. 이 때문에 복잡한 조합을 이용하는 경우 동적으로 쿼리를 생성해서 처리할 수 있는 기능이 필요합니다.<br>
Querydsl은 이러한 상황을 해결할 수 있는 기술입니다.

---
<br>

# 1. Querydls 사이트
---
<br>

![1](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/1.PNG)
<br>

Querydsl은 다양한 기능을 제공하는데 우리는 이 중 JPA 관련 부분을 적용하려 합니다.<br>

# 2. build.gradle 추가 - 1
---
<br>

![2](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/2.PNG)
<br>

위의 그림과 같이 주석처리한 부분을 추가로 작성합니다.<br>
queryDslVersion을 지정해주고 plugins 항목에 querydsl 관련 부분을 추가합니다.

# 3. build.gradle 추가 - 2
---
<br>

![3](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/3.PNG)
<br>

다음으로 dependencies에 주석처리한 부분을 추가로 작성합니다.<br>
중간에 잘린 부분은 importedProperties['querydsl.version']}:jakarta" 입니다.<br>
Querydsl을 위한 gradle의 task를 생성하기 위해 추가적으로 dependencies 밑에 코드를 작성합니다.<br>
코드 작성을 마치고 build.gradle 파일을 갱신합니다.<br>

# 4. compileQuerydsl 실행
---
<br>

![4](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/4.PNG)
<br>

갱신을 마치면 compileQuerydsl이라는 실행 가능한 task가 추가된 것을 확인할 수 있습니다.<br>
이 task를 실행해 본 뒤 실행 결과로 build 폴더 내에 generated 폴더가 생긴 뒤 QBaseEntity와 QGuestbook가 생성된 것을 확인할 수 있습니다.<br>


# 5. QGuestBook 확인
---
<br>

![5](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/5.PNG)
<br>

생성된 QGuestbook 클래스를 살펴보면 내부적으로 선언된 필드가 모두 변수로 처리되는 것을 확인할 수 있습니다.<br>
자동으로 생성되는 것이 의미하는건 Q 클래스를 개발자가 건드리지 않는다는 것입니다.<br>

# 6. QuerydslPredicateExcutor 상속
---
<br>

![6](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/6.PNG)
<br>

GuestbookRepository 인터페이스에 추가로 QuerydslPredicateExcutor를 상속하게 코드를 작성합니다.<br>
