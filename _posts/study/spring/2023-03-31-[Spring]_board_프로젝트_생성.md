---
layout: post
title: "[Spring] board 프로젝트 생성"
subtitle: Spring
date: '2023-03-31 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

하나의 엔티티가 아닌 여러 엔티티를 사용하는 프로젝트를 만들어봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
앞서 만든 Guestbook 프로젝트는 하나의 엔티티만을 사용해 기본적인 게시판 CRUD기능을 수행했습니다.<br>
이번엔 하나의 엔티티만을 사용하는 것이 아닌 회원, 게시글, 댓글 총 세 가지의 엔티티를 사용해 N:1 매핑을 처리해보려 합니다.<br>


---
<br>

# 1. 연관 관계와 관계형 데이터베이스 설계
---
<br>

![1](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/1.png)
<br>

엔티티를 여러개 사용한다는 것은 데이터 베이스에 테이블이 여러개 존재한다는 것을 의미합니다. 관계형 데이터베이스를 통해 이러한 테이블들의 연관관계를 구현하기 위해서 먼저 ER 다이어그램을 통해 테이블을 설계해야 합니다.<br>
이번 board 프로젝트에서는 위의 그림과 같은 다이어그램을 사용합니다.<br>
board 프로젝트에서 board는 member가 있어야만 작성될 수 있습니다. 먼저 member 테이블을 설계한 뒤 게시글과의 관계를 설정합니다.<br>
reply는 board가 있어야만 작성될 수 있습니다. 따라서 가장 나중에 설계하도록 합니다.<br>
board는 member와 n:1 관계를 가지고 reply는 board와 n:1 관계를 가집니다.<br>

# 2. BaseEntity 생성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/2.png)
<br>

[프로젝트_구조_만들기](https://heesung98.github.io/study/Spring-_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EA%B5%AC%EC%A1%B0_%EB%A7%8C%EB%93%A4%EA%B8%B0.html)에서 만든 방법대로 board라는 이름의 프로젝트를 생성합니다. build.gradle과 application.properties 또한 동일하게 작성합니다.<br>
그 뒤 프로젝트 내에 entity 패키지를 생성한 뒤 guestbook에서 사용한 BaseEntity를 동일하게 작성합니다.


# 3. BoardApplication 설정
---
<br>

![3](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/3.png)
<br>

생성된 BoardApplication에 `@EnableJpaAuditing`을 작성해 시간 처리를 수행하도록 합니다.<br>


# 4. Member 엔티티 클래스 추가
---
<br>

![4](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/4.png)
<br>

위에서 말했던 것 처럼 Member 엔티티부터 생성한 뒤 위의 그림과 같이 작성합니다.<br>
Member 클래스는 email을 PK로 사용합니다. Member 클래스는 별도의 FK를 사용하지 않습니다.<br>

# 5. Board 엔티티 클래스 추가
---
<br>

![5](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/5.png)
<br>

다음으로 Board 엔티티를 생성한 뒤 위의 그림과 같이 작성합니다.<br>
Board 클래스는 Member의 email을 FK로 참조해 사용합니다. 먼저 이를 작성하지 않은 뒤 나머지 필드부터 작성합니다.<br>

# 6. Reply 엔티티 클래스 추가
---
<br>

![6](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/6.png)
<br>

마지막으로 Reply 엔티티를 생성한 뒤 위의 그림과 같이 작성합니다.<br>
Reply 또한 Board와 연관관계를 작성하지 않은 채 나머지 항목 필드만 작성합니다.<br>

# 7. Board 엔티티 연관관계 설정
---
<br>

![7](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/7.png)
<br>

board 테이블과 member 테이블은 FK를 이용한 참조를 사용하게 됩니다. member의 email을 board가 FK로 참조하는 것입니다.<br>
이러한 연관관계를 설정할 때 `@ManyToOne` 어노테이션을 사용합니다. Member 클래스의 writer 필드를 작성한 뒤 @ManyToOne 어노테이션을 사용해 외래키 관계로 연결되게 합니다.<br>

# 8. Reply 엔티티 연관관계 설정
---
<br>

![8](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/8m.png)
<br>

마찬가지로 reply 테이블과 board 테이블의 PK를 참조하게 구성하도록 @ManyToOne 어노테이션을 사용해 Board 클래스의 board 클래스의 필드 board를 작성합니다.

# 9. 엔티티별 Repository 인터페이스 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-03-31-[Spring]_board_프로젝트_생성/9.png)
<br>

프로젝트 내에 위의 그림과 같은 경로로 repository 패키지를 만든 뒤 각 엔티티별 Repository 인터페이스를 작성합니다.<br>
