---
layout: post
title: "[Spring] Pageble 인터페이스를 통해 페이징과 정렬 처리하기"
subtitle: Spring
date: '2023-03-05 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

`Pageable 인터페이스`를 통해 `페이징`과 `정렬` 처리를 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

페이징 처리와 정렬은 SQL을 공부할 때 반드시 필요한 부분입니다. 페이지 처리는 DB에 따라서 사용되는 기법이 다른 경우가 많기 때문에 별도의 학습이 필요했습니다.<br>
JPA는 이런 처리를 `Dialect`를 통해 내부적으로 처리합니다. JPA는 SQL이 아닌 API의 객체와 메서드를 사용하는 형태로 페이징을 할 수 있게 합니다.<br>
`Pageable 인터페이스`는 페이지 처리에 필요한 정보를 전달하는 용도로 인터페이스이기 때문에 구현체인 `PageRequest`라는 클래스를 사용합니다.
앞서 [JpaRepository 인터페이스 및 테스트 코드를 통한 CRUD](https://heesung98.github.io/study/Spring-_Spring_Data_JPA%EB%A5%BC_%EC%9D%B4%EC%9A%A9%ED%95%98%EB%8A%94_%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8_%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0.html)에서 만든 프로젝트에 페이징과 정렬기능을 사용해보겠습니다.<br>

---
<br>

# 1. Pageable 인터페이스와 PageRequest
---
<br>

![1](/assets/img/web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/1.PNG)
<br>

페이징 테스트를 위한 testPageDefault() 메소드를 작성합니다.<br>
Pageable 인터페이스를 통해 pageable 변수를 만든 뒤 PageRequest.of() 메소드를 통해 구현합니다. PageRequest.of(0, 10)은 0번 부터 시작하는 size가 10인 페이지를 의미합니다. PageRequest.of()는 리턴타입으로 Page 타입을 반환합니다.<br>
그 후 Page<엔티티 타입> 객체인 result를 생성한 후 해당 객체에 findAll(pageable) 메소드의 리턴값을 받습니다.<br>
해당 테스트 코드를 실행한 뒤 스택트레이스를 확인하면 MariaDB의 페이징 처리 구문인 limit가 사용되는 것을 확인할 수 있고 두 번째 쿼리에서 count()를 이용해 전체 개수를 처리하는 것을 확인할 수 있습니다.

# 2. Page<Entity>의 여러 메소드
---
<br>

![2](/assets/img/web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/2.PNG)
<br>

Page<Entity>의 경우 쿼리 결과를 확인하기 위한 여러 메소드를 지원합니다.<br>
스택트레이스에 출력된 결과를 통해 메소드가 반환하는 결과가 무엇을 의미하는지 이해할 수 있을 것입니다.

# 3. getContent()
---
<br>

![3](/assets/img/web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/3.PNG)
<br>

실제 페이지의 데이터를 확인하는 것은 getContent()를 통해 List<엔티티 타입>으로 처리하거나 Stream<엔티티 타입>을 반환하는 get()을 이용할 수 있습니다.<br>
result.getContent()의 반환값을 Memo타입의 memo에 담아 하나씩 출력하는 것을 확인할 수 있습니다.


# 4. 페이지 정렬 조건 추가하기
---
<br>

![4](/assets/img/web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/4.PNG)
<br>

PageRequest.of()의 세 번째 매개변수로 Sort타입을 전달할 수 있습니다.<br>
Sort타입의 객체 sort1을 만듭니다. sort1은 Sort.by() 메소드를 통해 memoNo을 기준으로 역순으로 정렬하게 합니다.<br>
스택트레이스를 통해 확인해보면 역순으로 잘 정렬된 것을 확인할 수 있습니다.

# 5. MemoRepository 인터페이스 생성하기
---
<br>

![5](/assets/img/web/spring/2023-03-05-[Spring]_Pageable_인터페이스를_통해_페이징과_ 정렬_ 처리하기/5_m.PNG)
<br>

정렬 조건은 Sort 객체의 and() 메소드를 통해 여러 개의 정렬 조건을 다르게 설정할 수 있습니다. memoNo은 des로, memoText는 asc로 sort1과 sort2를 만든 뒤 sortAll에서 and() 메소드를 통해 연결할 수 있습니다.<br>
