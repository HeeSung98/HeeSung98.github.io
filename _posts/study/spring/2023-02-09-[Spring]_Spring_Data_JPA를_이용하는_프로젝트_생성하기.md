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

`JPA`는` ORM(Obejct Relational Mapping)` 기술에 대한 API 표준 명세이고 ORM이란 객체와 관계형 데이터 베이스를 매핑해주는 기술입니다. JPA는 실제로 동작하는 것이 아닌 인터페이스 모음입니다.<br>

이러한 JPA를 실제로 구현해주는 것은 `Hibernate`입니다. Hibernate는 ORM의 프레임워크이자 JPA의 구현체입니다.<br>

우리가 최종적으로 사용할 `Spring Data JPA`란 `JPA`를 사용하기 편하도록 만들어놓은 모듈입니다.<br>

Spring Data JPA는 `Repository 인터페이스`를 제공하며 이를 통해 간단하게 데이터 접근을 가능하게 합니다.<br>

[MySQL_Workbench_시작하기](https://heesung98.github.io/study/MariaDB-_MySQL_Workbench_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0.html) 에서 생성한 데이터베이스를 스프링부트 프로젝트에서 사용해 보겠습니다.<br>

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

생성한 프로젝트에 entity 패키지를 추가하고 Memo라는 클래스를 생성하고 Memo클래스의 내용은 위와 같이 작성합니다.<br>
Memo 클래스는 엔티티 클래스로 데이터베이스의 테이블과 같은 구조입니다.<br>
Spring Data JPA를 사용하기 위해서는 반드시 `@Entity` 어노테이션을 추가해야 합니다. @Entity 어노테이션을 추가하면 이 클래스가 엔티티를 위한 클래스임을 나타냅니다.<br>
`@Table` 어노테이션을 사용하면 이 클래스가 어떠한 테이블인지의 정보를 담을 수 있습니다.
해당 어노테이션의 매개변수로 name="t_memo"가 들어갔는데 이는 테이블의 이름이 t_memo임을 뜻합니다.<br>
`@Id` 어노테이션은 해당 어노테이션의 필드 값을 Primary Key로 지정합니다.<br>
`@GeneratedValue` 어노테이션을 사용하면 PK를 자동으로 생성합니다.<br>

**엔티티 클래스를 작성할 때 ID의 이름으로 m_no를 사용했는데 이렇게 엔티티를 작성할 시 자바에서는 메소드의 매개변수로 '_'를 넘기지 못하기 때문에 추후에 오류가 생길 수 있습니다. 따라서 저는 이 엔티티 ID를 memoNo으로 변경하였습니다.**<br>

<br>

# 7. 엔티티 클래스 수정
---
<br>

![7](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/7.PNG)

작성한 엔티티 클래스에 기능을 추가적으로 더 부여하겠습니다.<br>
`@Column` 어노테이션을 사용해 컬럼의 속성을 지정할 수 있습니다. t_memo 테이블의 memoText 컬럼의 경우 null이 들어갈 수 없고 길이는 200자로 제한됩니다.<br>
`@Getter` 어노테이션과 `@Builder` 어노테이션을 이용해 Getter 메서드를 생성하고 객체를 생성할 수 있게 합니다.<br>
@Builder를 사용하기 위해서는 `@AllArgsConstructor`와 `@NoArgsConstructor`를 같이 사용해야 컴파일 에러가 발생하지 않습니다.

<br>

# 8. JPA 관련 apllication.properties 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/8m.PNG)

apllication.properties에 JPA 사용에 관련된 항목을 추가하겠습니다.<br>
`spring.jpa.hibernate.ddl-auto=update`: 프로젝트 실행 시 자동으로 DDL(Data Definition Language)을 생성할 것을 정하는 것입니다.<br>
`spring.jpa.properties.hibernate.format_sql=true`: Hibernates를 통해 생성된 SQL을 스택트레이스에 출력하도록 설정합니다.<br>
`spring.jpa.show-sql=true`: JPA 처리 시 생성되는 SQL을 보이게 할 것인지 설정합니다.

<br>

# 9. 데이터베이스와의 연동 확인
---
<br>

![9](/assets/img/study_Web/spring/2023-02-08-[Spring]_Spring_Data_JPA를_이용하는_프로젝트_생성하기/9.PNG)

이러한 설정들을 모두 마친 뒤 프로젝트를 실행한 뒤 tbl_memo 테이블이 생성된 것을 MySQL Workbench를 통해 확인할 수 있습니다.

<br>

