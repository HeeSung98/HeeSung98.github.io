---
layout: post
title: "[Spring] JpaRepository 인터페이스 및 테스트 코드를 통한 CRUD"
subtitle: Spring
date: '2023-02-10 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`JpaRepository 인터페이스`를 활용해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

`Spring Data JPA`는 JPA의 구현체인 `Hibernate`를 사용하기 위해 `JpaRepository 인터페이스`를 제공합니다. 이러한 JpaRepository 인터페이스를 통해 CRUD, 페이징, 정렬 등 여러 작업을 `메서드를 호출하는 형태`로 처리합니다.<br>

Spring Data JPA는 JpaRepository를 상속하는 것 만으로 모든 처리를 끝나게 하는 편리함을 제공합니다.<br>

실제 동작 시에는 스프링이 내부적으로 해당 인터페이스에 맞는 코드를 생성합니다.<br>

**엔티티 클래스를 작성할 때 ID의 이름으로 m_no를 사용했는데 이렇게 엔티티를 작성할 시 자바에서는 메소드의 매개변수로 '_'를 넘기지 못하기 때문에 추후에 오류가 생길 수 있습니다. 따라서 저는 이 엔티티 ID를 memoNo으로 변경하였습니다.**<br>

---
<br>

# 1. MemoRepository 인터페이스 생성하기
---
<br>

![1](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/1.PNG)
<br>

JpaRepository 인터페이스를 사용하기 위해 [Spring Data JPA를 이용하는 프로젝트 생성하기](https://heesung98.github.io/study/Spring-_Spring_Data_JPA%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0.html)에서 생성한 프로젝트 내에 repository 패키지를 생성하고, MemoRepository 인터페이스를 추가합니다.<br>

MemoRepository는 JpaRepository 인터페이스를 상속하는 것이 전부입니다. 이 때 엔티티의 타입 정보와 PK인 @Id의 타입을 지정합니다.<br>

Spring Data JPA는 위와같은 인터페이스의 선언만을 통해 스프린의 빈(bean)에 등록됩니다.<br>

스프링이 내부적으로 인터페이스 타입에 맞게 객체를 생성해 빈으로 등록합니다.<br>

# 2. MemoRepository 인터페이스의 테스트 코드 생성하기 
---
<br>

![2](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/2.PNG)
<br>

Memorpository를 이용해서 생성된 테이블에 SQL 없이 CRUD 처리를 테스트하기 위한 코드를 작성합니다.<br>
프로잭트 생성 시에 만들어진 test 폴더에 repository 패키지를 작성하고 MemoRepositoryTests 클래스를 생성합니다.<br>

# 3. MemoRepository가 정상적으로 처리되고 있는지 확인
---
<br>

![3](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/3.PNG)
<br>

본격적인 CRUD 테스트에 앞서 MemoRepository가 정상적으로 스프링에서 처리되고 의존성의 문제가 없는지 확인하는 코드를 작성하겠습니다.<br>
 Test코드를 실행하면 스프링이 memoRepository 클래스를 자동으로 생성하고 이 때 생성된 클래스의 이름을 확인해 보고자 합니다. 스택트레이서에 표시해둔 부분을 살펴보면 'jdk.proxy3.$Proxy111'와 같이 생성한 적이 없는 클래스의 이름이 출력되고 있는 것을 볼 수 있습니다.<br>
  이는 동적 프록시 방식으로 만들어 진 것이며 정상적으로 스프링에서 처리되고 있는 것을 확인할 수 있습니다.<br>

# 4. 등록 작업 테스트
---
<br>

![4](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/4.PNG)
<br>

등록 작업 테스트는 `save(엔티티 객체)` 메서드를 사용합니다.<br>
testInsertDummies()는 100개의 Memo 객체를 생성하고 이를 save 메서드의 매개변수로 넘겨 insert 하는 것입니다.<br>
memoText는 Not Null이기 때문에 반드시 데이터를 삽입합니다.<br>
스택트레이서를 확인하면 Hibernate가 발생하는 insert를 확인할 수 있습니다.<br>

# 5. 등록 작업 테스트 결과 확인
---
<br>

![5](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/5.PNG)
<br>

MySQL workbench를 통해 확인해서 등록 작업의 최종 결과를 조회해 확인합니다. 100개의 튜플이 생성된 것을 확인할 수 있습니다.<br>

# 6. 조회 작업 테스트
---
<br>

조회 작업은 `findById(키 타입)`, `getOne(키 타입)` 메서드를 사용합니다.<br>
findById()와 getOne()은 동작 방식에서 데이터베이스를 먼저 사용하는가 나중에 사용하는가의 차이가 있습니다.<br>
우선 findById()를 살펴보겠습니다.<br>

# 7. 조회 작업 테스트(findeById()) 결과 확인
---
<br>

![6](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/6.PNG)
<br>

findById()의 실행 결과를 살펴보면 findById()를 실행하는 순간 SQL은 처리가 된 후 println("===")이 실행되는 것을 볼 수 있습니다.<br>
다음으로 getOne()을 살펴보겠습니다.<br>

# 8. 조회 작업 테스트(getOne()) 결과 확인
---
<br>

![7](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/7.PNG)
<br>
getOne()의 경우 @Transactional 어노테이션이 필요합니다. @Transactional은 트랜잭션 처리를 위한 어노테이션 입니다.<br>
findById()의 테스트 결과와 비교해 보면 getOne()을 호출한 후 println("===")이 실행되면서 memo 객체를 실제로 사용하는 순간 SQL이 실행되는 것을 확인할 수 있습니다.<br>

# 9. 수정 작업 테스트
---
<br>

![8](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/8.PNG)
<br>

수정 작업 테스트는 등록 작업과 같은 `save(엔티티 객체)` 메서드를 사용합니다.<br>

testUpdate()를 살펴보면 m_no이 Long타입의 100인 객체를 만든 뒤 save()를 호출합니다. 이 때 내부적으로는 해당 객체의 @Id값과 동일한 객체가 있다면 update를 수행하고 존재하지 않다면 insert를 실행하게 됩니다.<br>

<br>

# 10. 수정 작업 테스트 결과 확인
---
<br>

![9](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/9.PNG)
<br>

데이터베이스의 100번째 튜플이 정상적으로 수정된 것을 확인할 수 있습니다.


<br>

# 11. 삭제 작업 테스트
---
<br>

![10](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/10.PNG)
<br>

마지막으로 삭제 작업은 `deleteById(키 타입)`, `delete(엔티티 객체)` 메서드를 사용합니다.<br>
삭제 작업도 수정과 동일한 개념으로 삭제하려는 번호의 엔티티 객체가 있는지 먼저 확인한 뒤 삭제를 수행합니다.<br>

<br>

# 12. 삭제 작업 테스트 결과 확인
---
<br>

![11](/assets/img/study_Web/spring/2023-02-10-[Spring]_JpaRepository_인터페이스_및_테스트_코드를_통한_CRUD/11.PNG)
<br>

데이터베이스의 100번째 튜플이 정상적으로 삭제된 것을 확인할 수 있습니다.


<br>



