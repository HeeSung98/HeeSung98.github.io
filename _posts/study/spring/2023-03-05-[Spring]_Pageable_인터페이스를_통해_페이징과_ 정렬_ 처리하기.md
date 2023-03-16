---
layout: post
title: "[Spring] Pageble 인터페이스를 통해 페이징과 정렬 처리하기"
subtitle: Spring
date: '2023-03-05 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Pageble 인터페이스`를 통해 `페이징`과 `정렬` 처리를 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

페이징 처리와 정렬은 SQL을 공부할 때 반드시 필요한 부분입니다. 페이지 처리는 DB에 따라서 사용되는 기법이 다른 경우가 많기 때문에 별도의 학습이 필요했습니다.<br>
JPA는 이런 처리를 `Dialect`를 통해 내부적으로 처리합니다. JPA는 SQL이 아닌 API의 객체와 메서드를 사용하는 형태로 페이징을 할 수 있게 합니다.<br>
앞서 [JpaRepository 인터페이스 및 테스트 코드를 통한 CRUD](https://heesung98.github.io/study/Spring-_Spring_Data_JPA%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0.html)에서 만든 프로젝트에 페이징과 정렬기능을 추가하겠습니다.

---
<br>

# 1. MemoRepository 인터페이스 생성하기
---
<br>

![1](/assets/img/study_Web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/1.PNG)
<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>

# 2. MemoRepository 인터페이스 생성하기
---
<br>

![2](/assets/img/study_Web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/2.PNG)
<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>

# 3. MemoRepository 인터페이스 생성하기
---
<br>

![2](/assets/img/study_Web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/3.PNG)
<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>


# 4. MemoRepository 인터페이스 생성하기
---
<br>

![4](/assets/img/study_Web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/4.PNG)
<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>

# 5. MemoRepository 인터페이스 생성하기
---
<br>

![5](/assets/img/study_Web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/5.PNG)
<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>
