---
layout: post
title: "[Spring] 엔티티 테스트 및 Querydsl 테스트"
subtitle: Spring
date: '2023-03-21 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

생성한 프로젝트의 엔티티와 Querydsl의 테스트를 수행해 봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
JpaRepository의 기능들은 이미 살펴보았으니 Querydsl을 위주로 테스트를 진행하겠습니다.<br>

---
<br>

# 1. GuestbookRepositoryTests 클래스 추가
---
<br>

![1](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/1.PNG)
<br>

테스트를 위해 test 폴더 내에 repository 패키지를 생성한 뒤 GuestbookRepositoryTests 클래스를 추거합니다.<br>
GuestbookRepositoryTests 클래스의 코드는 위와 같습니다.<br>
테스트를 위해 300개의 테스트 데이터를 넣는 insertDummies()의 코드 또한 작성한 뒤 실행합니다.<br>

# 2. insertDummies() 결과 확인
---
<br>

![2](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/2.PNG)
<br>

데이터베이스를 살펴본 결과 300개의 데이터가 추가된 것을 확인할 수 있으며 moddate와 regdate 역시 모두 채워지는 것을 확인할 수 있습니다.<br>

# 3. 엔티티 setter 메서드 추가
---
<br>

![3](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/3.PNG)
<br>

엔티티 클래스는 setter 관련 기능을 만들지 않는 것을 권장합니다만 필요에 따라서는 수정 기능을 만들기도 합니다. 엔티티 객체가 애플리케이션 내부에서 변경되면 JPA를 관리하는 쪽이 복잡해질 우려가 있기 때문에 가능하면 최소한의 수정이 가능하다록 하는 것을 권장합니다.<br>
이번에 만들 Guestbook은 수정 기능이 없어도 무방하지만 수정 시간이 정상적으로반영 되는지 확인하기 위해 수정 기능을 위의 그림과 같이 추가합니다.<br>


# 4. 수정 시간 테스트
---
<br>

![4](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/4.PNG)
<br>

수정 시간이이 정상적으로 반영되는지 확인하기 위한 updateTest() 메소드를 위의 그림과 같이 작성합니다.<br>
findById()를 통해 optional \<Guestbook\>타입의 객체 result에 담아와 result의 정보를 Guestbook 타입의 객체 guestbook에 옮겨담은 뒤 changeTitle(), changeContent()를 통해 값을 변경한 후 save()로 저장합니다. 

# 5. 수정 시간 테스트 결과
---
<br>

![5](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/5.PNG)
<br>

updateTest()를 실행한 결과 수정 시간이 정상적으로 반영되고 있는 것을 확인할 수 있고 Title과 Content의 내용 또한 정상적으로 변경된 것을 확인할 수 있습니다.

# 6. Querydsl 단일 항목 검색 테스트
---
<br>

![6](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/6.PNG)
<br>

우리가 게시글을 검색할 때 '제목/내용/작성자' or '제목 + 내용' / '제목 + 작성자' / '내용 + 작성자' or '제목 + 내용 + 작성자' 와 같은 방법으로 검색합니다. 엔티티 클래스에 멤버 변수가 많이 선언되어 있다면 조합의 수가 많아집니다. 이럴 때 Querydsl은 상황에 맞게 쿼리를 처리할 수 있게 해줍니다.<br>
먼저 제목에 1이라는 글자가 있는 엔티티를 검색하는 테스트는 위의 코드와 같습니다.<br>
사이즈가 10인 역순으로 정렬하는 페이지를 만든 뒤 Q도메인 클래스의 객체 qGuestbook을 선언합니다. Q도메인 클래스를 통해 엔티티 클래스의 title, content와 같은 필드를 변수로 사용할 수 있습니다.<br>
BooleanBuilder 클래스의 객체 builder를 만듭니다. BoolenBuilder는 where문에 들어가는 조건을 담는 컨테이너라고 생각하면 되겠습니다.<br>
원하는 조건은 필드 값과 같이 결합해서 생성합니다. BooleanBuilder 안에 들어가는 값은 com.querydsl.core.types.Predicate 타입입니다.<br>
만들어진 조건은 where문에 and나 or같은 키워드와 결합합니다.<br>
BooleanBuilder는 GuestbookRepository에 추가된 QuerydslPredicateExcutor 인터페이스의 findAll()을 사용합니다.<br>
위 그림과 같은 testQuery1 코드를 작성한 뒤 테스트합니다.<br>



# 7. Querydsl 단일 항목 검색 테스트 실행 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/7.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>
쿼리의 중간부분을 살펴보면 where 조건절에서 title에 대한 처리가 진행되는 것을 볼 수 있습니다.<br>

# 8. Querydsl 다중 항목 검색 테스트
---
<br>

![8](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/8.PNG)
<br>

다중 항목을 검색하기 위해 testQuery2 코드를 작성합니다.<br>
7번 그림과 유사하지만 BooleanExperssion 변수가 하나에서 exTitle과 exContent, exAll 세 개로 늘어난 것을 확인할 수 있습니다. exTitle과 exContent는 7번 그림과 유사하게 사용되지만 exAll은 exTitle과 exContent를 or로 결합하는 것을 알 수 있습니다. 또한 bulder.and()를 통해 gno가 0보다 크다라는 조건을 추가한 것을 알 수 있습니다.<br>

# 9. Querydsl 다중 항목 검색 테스트 실행 결과
---
<br>

![9](/assets/img/study_Web/spring/2023-03-21-[Spring]_엔티티_테스트_및_Querydsl_테스트/9.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>
쿼리 중간의 where절 내부에 or문으로 like문 두 개가 결합된 것을 확인할 수 있습니다.<br>
만약 제목 + 내용에 작성자 또한 처리하고자 한다면 BooleanExpression을 추가로 생성한 뒤 or 조건으로 결합합니다.<br>
