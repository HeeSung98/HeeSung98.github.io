---
layout: post
title: "[Spring] 쿼리 메소드 기능과 @Query"
subtitle: Spring
date: '2023-03-08 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

`쿼리 메소드`와 `@Query`를 통해 쿼리문을 처리해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

앞의 글에서 사용했던 방법으로만 쿼리문을 처리할 때 다양한 검색 조건을 사용할 수 없는 부분이 아쉬웠습니다. 이러한 부분을 해결하기 위해 Spring Data JPA는 `쿼리 메소드`와 `@Query`, `Querydsl`과 같은 방법을 제공합니다. 우선 쿼리 메소드와 @Query를 사용한 처리를 수행해보겠습니다.<br>
앞서 [JpaRepository 인터페이스 및 테스트 코드를 통한 CRUD](https://heesung98.github.io/study/Spring-_Spring_Data_JPA%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0.html)에서 만든 프로젝트에 페이징과 정렬에 이어 쿼리 메소드와 @Query를 추가하겠습니다.<br>

---
<br>

# 1. findBy 쿼리 메소드
---
<br>

![1](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/1.PNG)
<br>

쿼리 메소드는 메소드의 이름 자체가 쿼리가 되는 기능입니다. 쿼리 메소드는 주로 findBy 또는 getBy로 시작하고 필요한 필드 조건이나 And, Or와 같은 키워드를 이용해 쿼리문을 만듭니다.<br>
쿼리 메소드는 MemoRepository 인터페이스에 작성해 사용합니다. <br>
findByMemonoBetweenOrderByMemonoDesc() 메소드의 이름을 살펴보면 memoNo를 기준으로 between을 수행하고 내림차순으로 정렬하는 것을 알 수 있습니다.<br>

# 2. findByMemonoBetweenOrderByMemonoDesc() 테스트
---
<br>

![2](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/2.PNG)
<br>

testQueryMethods()를 살펴보면 Memo 객체의 memoNo값이 70에서 80사이의 객체를 구한 뒤 역순으로 정렬합니다.<br>
해당 리스트를 출력해 스택트레이스에서 확인하면 정상적으로 쿼리문이 수행된 것을 확인할 수 있습니다.<br>

# 3. 쿼리 메소드와 Pageable의 결합
---
<br>

![3](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/3.PNG)
<br>

쿼리 메소드를 사용할 때 정렬 기능을 사용하려면 위의 예시와 같이 OrderBy 키워드를 사용하기 때문에 메소드의 이름이 길고 혼동하기 쉬운 단점이 있습니다. 쿼리 메소드는 이러한 문제를 Pageable과 결합해서 사용해 해결합니다.<br>
위의 코드를 살펴보면 메소드의 이름이 OrderBy부터 존재하지 않고 매개변수로 Pageable이 추가된 것을 확인할 수 있습니다.<br>


# 4. findByMemonoBetween() 테스트
---
<br>

![4](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/4.PNG)
<br>

testQueryMethodsWithPageable()을 살펴보면 memoNo을 기준으로 내림차순 정렬하고 size가 10인 1번 페이지를 생성한 뒤 이 페이지를 findByMemonoBetween()의 매개변수로 사용합니다.<br>
해당 테스트 코드의 출력을 스택트레이서에서 확인해보면 40번부터 31번까지 역순으로 출력되는 것을 확인할 수 있습니다.<br>

# 5. 쿼리 메소드 자동완성
---
<br>

![5](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/5.PNG)
<br>

Intellij의 경우 쿼리 메소드를 작성할 때 자동완성 기능을 지원하기 때문에 수월하게 사용할 수 있습니다.<br>

# 6. deleteBy 쿼리 메소드
---
<br>

![6](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/6.PNG)
<br>

쿼리 메소드를 통해 삭제를 할 때 deleteBy를 사용합니다.<br>
deleteMemoByMemonoLessThan()은 메소드의 이름을 통해 memoNo보다 작은 데이터를 삭제할 때 사용한다는 것을 알 수 있습니다.


# 7. deleteMemoByMemonoLessThan() 테스트
---
<br>

![7](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/7.PNG)
<br>

테스트 코드를 살펴보면 `@Transactional`과 `@Commit`이라는 어노테이션을 사용합니다.<br>
이는 deleteBy의 경우 select문으로 해당 엔티티를 가져오는 작업과 삭제하는 과정이 같이 이루어지기 때문입니다.<br>
@Commit은 최종 결과를 커밋하기 위해 사용됩니다. 이를 사용하지 않으면 테스트 코드의 deleteBy는 롤백처리되기 때문에 결과가 반영이 되지 않습니다.<br>
deleteBy는 실무에서는 많이 사용되지 않는데 스택트레이스에서 보이는 것과 같이 각 엔티티를 하나씩 삭제하기 때문입니다.<br>

# 8. deleteMemoByMemonoLessThan() 결과 확인
---
<br>

![8](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/8.PNG)
<br>

MySQL Workbench를 통해 확인해본 결과 99번을 제외한 모든 데이터가 삭제된 것을 확인할 수 있습니다.<br>

# 9. @Query 어노테이션
---
<br>

![9](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/9.PNG)
<br>

Spring Data JPA가 제공하는 쿼리 메소드는검색과 같은 기능을 수행할 때 편리하지만 조인이나 복잡한 조건을 처리할 때 불편할 때가 많습니다. 때문에 간단한 처리만 수행할 때 쿼리 메소드를 사용하고 일반적인 경우 @Query를 이용하는 경우가 더 많습니다.<br>
@Query 또한 쿼리 메소드와 마찬가지로 MemoRepository에 작성하였고 위의 코드를 살펴보면 사용 예시를 확인할 수 있습니다.<br>
@Query의 경우 value값으로 `JPQL(Java Persistence Query Language)`을 사용하며 JPQL은 객체지향 쿼리라고 불립니다.<br>

# 10. updateMemoText2() 테스트
---
<br>

![10](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/10.PNG)
<br>

MemoRepository에 작성하였던 @Query중 updateMemoText2()에 대한 테스트를 해보겠습니다.<br>
Memo의 객체 memo를 bulider()를 통해 생성합니다. memoNo은 99이고 memoText는 "queryAnnotationTest"로 적겠습니다. 그 후 updateMemoText2()의 매개변수로 memo를 넘겨준 뒤 수행하면 테스트 코드가 정상적으로 작동된 것을 확인할 수 있습니다.<br>

# 11.  updateMemoText2() 결과 확인
---
<br>

![11](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/11.PNG)
<br>

MySQL Workbench를 통해 확인해본 결과 99번 데이터의 내용이 memo의 내용으로 업데이트된 것을 확인할 수 있습니다.<br>

# 12. getNativeResult() 테스트
---
<br>

![12](/assets/img/web/spring/2023-03-08-[Spring]_쿼리_메소드_기능과_@Query/12.PNG)
<br>

마지막으로 getNativeResult()의 테스트를 수행해보겠습니다.<br>
List타입의 객체 list에 getNativeResult()의 결과를 담은 뒤 출력합니다. 출력의 결과로 스택트레이서에 99, queryAnnotationTest이 정상적으로 나오는 것을 확인할 수 있습니다.<br>
