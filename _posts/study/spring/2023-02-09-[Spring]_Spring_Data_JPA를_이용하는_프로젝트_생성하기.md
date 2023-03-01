---
layout: post
title: "[Spring] Spring Data JPA를 이용하는 프로젝트 생성하기"
subtitle: Spring
date: '2023-02-09 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Spring Data JPA`를 이용하는 프로젝트를 생성하고 실행해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

`Spring Data JPA`란 <br>

---
<br>

[MySQL_Workbench_시작하기](https://heesung98.github.io/study/MariaDB-_MySQL_Workbench_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0.html) 이 글에서 생성한 데이터베이스를 스프링부트 프로젝트에서 사용해 보겠습니다.<br>

---
<br>


# 1. 새 프로젝트 만들기
---
<br>

![1](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/1.PNG)

<br>

# 2. 의존성 선택
---
<br>

![2](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/2.PNG)

프로젝트에 추가할 의존성은 그림의 빨간색 상자를 통해 확인할 수 있습니다. 데이터베이스를 활용하기 위해서는 반드시 'Spring Data JPA'의존성을 추가해야 합니다.

<br>

# 3. 생성된 프로젝트의 build.gradle에 라이브러리 추가
---
<br>

![3](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/3.PNG)

처음 생성한 프로젝트와는 달리 이번에 생성한 프로젝트는 Ex2Application을 실행할 경우 에러 메시지가 출력됩니다. 프로젝트 내에 Spring Data JPA 라이브러리가 추가됐기 때문에 자동적으로 설정은 추가되었으나 구체적인 값이 지정되지 않아서 발생하는 문제입니다.<br>
이를 해결하기 위해 build.gradle에 `implementation 'mysql:mysql-connector-java:8.0.31'`을 작성하겠습니다. MySQL Connector를 사용해 스프링 프로젝트와 데이터베이스를 연동할 수 있습니다.

<br>

# 4. 스프링 프로젝트 데이터베이스 설정
---
<br>

![4](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/4m.PNG)
application.properties 파일에 생성한 프로젝트의 엔드포인트와 master-id, password를 작성합니다.


<br>

# 5. 프로젝트 실행이 정상적으로 되는지 확인
---
<br>

![5](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/5.PNG)
build.gradle과 application.properties 두 가지 파일을 수정한 뒤 Ex2Application을 실행한다면 정상적으로 프로젝트가 실행되는 것을 확인할 수 있습니다.

<br>

# 6. 엔티티 클래스 작성
---
<br>

![6](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/6.PNG)

<br>

# 7. 엔티티 클래스 수정
---
<br>

![7](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/7.PNG)

<br>

# 8. JPA 관련 apllication.properties 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/8.PNG)

<br>

# 9. 데이터베이스와의 연동 확인
---
<br>

![9](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/9.PNG)

<br>

