---
layout: post
title: "[Spring] JPQL을 이용한 검색"
subtitle: Spring
date: '2023-04-09 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

JPQL을 이용해 검색 처리를 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
board 프로젝트를 구성할 때 3개의 엔티티를 사용했습니다. board와 reply는 FK를 이용해 @ManyToOne과 같은 연관관계를 설정했습니다. guestbook과 달리 여러 엔티티 타입을 사용할 때 JPQL문을 이용한 검색은 조금 더 복잡해집니다. 여러 엔티티 타입을 JPQL로 처리한 결과물은 Object[] 타입, 즉 튜플로 나오기 때문에 복잡합니다. 복잡한만큼 어떤 상황에서도 사용할 수 있기 때문에 유용합니다.<br>
현재 작성중인 board 프로젝트는 Querydsl 설정이 없는 상태이기 때문에 Querydsl의 설정을 다시 해주어야 합니다.

---
<br>

# 1. Querydsl 설정
---
<br>

![1](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/1.png)
<br>

Querydsl의 설정은 앞서 작성한 글인 [동적 쿼리 처리를 위한 Querydsl 설정](https://heesung98.github.io/study/Spring-_%EB%8F%99%EC%A0%81_%EC%BF%BC%EB%A6%AC_%EC%B2%98%EB%A6%AC%EB%A5%BC_%EC%9C%84%ED%95%9C_Querydsl_%EC%84%A4%EC%A0%95.html)에서 확인할 수 있습니다. <br>
실행 환경에 따라 여러 오류들이 생길 수 있으니 설정을 바꿔가며 수행합니다.<br>

# 2. SearchBoardRepository 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/2.png)
<br>

`QuerydslRepositorySupport`를 이용해 검색 기능을 구현하고자 합니다. 이를 위해 repository 패키지 내에 search 패키지를 생성한 뒤 SearchBoardRepository 인터페이스를 작성합니다.<br>
SearchBoardRepository에는 Board 타입 객체를 반환하는 메소드 하나를 선언합니다.<br>


# 3. SearchBoardRepositoryImpl 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/3.png)
<br>

SearchBoardRepository 인터페이스의 구현 클래스 SearchBoardRepositoryImpl를 작성합니다.<br>
SearchBoardRepositoryImpl은 QuerydslRepositorySupport를 상속해 작성합니다. QuerydslRepositorySupport는 생성자가 존재하기 때문에 super()를 이용해 호출합니다.<br>
SearchBoardRepository에 작성한 search1()의 구현 역시 작성합니다. 동작이 제대로 되는지 여부를 확인하기 위해 우선 log.info를 사용해 작성합니다.<br>

# 4. BoardRepository 수정
---
<br>

![4](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/4.png)
<br>

BoardRepository에 SearchBoardRepository를 상속하는 형태로 수정합니다.<br>

# 5. BoardRepository testSearch() 작성 및 결과
---
<br>

![5](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/5.png)
<br>

Repository의 확장이 정상적으로 처리된 것을 확인할 수 있습니다.

# 6. SearchBoardRepositoryImpl search1() 작성
---
<br>

![6](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/6.png)
<br>

Querydsl 라이브러리 내에 JPQLQuery 인터페이스를 활용해 search1()을 작성합니다.<br>
QBoard타입의 board와 JPQLQuery 객체를 생성하는 것을 확인할 수 있습니다.<br>

# 7. BoardRepository testSearch() 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/7.png)
<br>

search1()의 테스트 결과를 살펴보면 SQL문이 실행되고 있는 것을 확인할 수 있습니다.<br>
선을 통해 구분해둔 부분에서 출력된 결과문을 살펴보면 JPQL의 문자열과 동일한 것과 실제 동작하는 SQL문을 확인할 수 있습니다.

# 8. SearchBoardRepositoryImpl search1() join(reply) 추가
---
<br>

![8](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/8.png)
<br>

JPQLQuery를 통해 join을 처리할 때 join()과 on()을 사용합니다.<br>
QReply타입의 reply를 추가한 뒤 leftJoin()과 on()을 사용합니다.

# 9. BoardRepository testSearch() 결과
---
<br>

![9](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/9.png)
<br>

join을 추가한 search1()의 결과를 살펴보면 SQL문에 left outer join이 추가된 것을 알 수 있습니다.

# 10. SearchBoardRepositoryImpl search1() join(member) 추가
---
<br>

![10](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/10.png)
<br>

QMember타입의 member를 추가한 뒤 한번 더 join합니다. 그 다음 groupBy()를 사용해 select()의 결과물에서 여러 객체를 가져오게 변경합니다.<br>
정해진 엔티티 단위가 아닌 데이터를 추출한 형태로 가져왔고 이 때 Tuple이라는 객체를 사용해 데이터를 받아와야 합니다.

# 11. SearchBoardRepositoryImpl search1() Tuple 사용
---
<br>

![11](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/11.png)
<br>

select()의 결과를 JPQLQuery\<Tuple\>을 이용해 처리하도록 변경하고 result 변수 역시 List\<Tuple\> 타입으로 변경했습니다.

# 12. BoardRepository testSearch() 결과
---
<br>

![12](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/12.png)
<br>

testSearch의 실행 결과는 위의 그림과 같습니다.<br>



# 13. 
---
<br>

![13](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/13.png)
<br>

gno를 눌러 read 페이지로 가는 것 또한 12번과 같이 type과 keyword를 추가해 처리합니다.<br>

# 14. 
---
<br>

![14](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/14.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 결과를 반영하는지 확인합니다.<br>
글 제목에 10이 들어간 방명록을 조회한 뒤 2번 페이지로 이동한 결과 정상적으로 페이지의 이동에 type과 keyword가 반영된 것을 확인할 수 있습니다.

# 15. 
---
<br>

![15](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/15.png)
<br>

gno 링크를 통한 read 페이지 이동이 검색 조건을 반영하는지 확인합니다.<br>
제목에 wow를 검색한 뒤 read 페이지로 이동한 결과 정상적으로 type과 keyword가 반영된 것을 확인할 수 있습니다.

# 16. 
---
<br>

![16](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/16.png)
<br>

조회 페이지에서 목록 페이지로 돌아갈 때 또한 검색 조건을 유지하도록 추가합니다.<br>
read.html의 Modify와 ToList 버튼에 type과 keyword를 넘기도록 작성합니다.<br>

# 17. 
---
<br>

![17](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/17.png)
<br>

Modify와 ToList버튼의 링크를 브라우저의 개발자 도구를 통해 확인한 결과 정상적으로 링크가 적용된 것을 확인할 수 있습니다.

# 18. 
---
<br>

![18](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/18.png)
<br>

수정 페이지 또한 조회 페이지로 이동할 때 검색 조건을 유지하도록 수정합니다.<br>

# 19. 
---
<br>

![19](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/19.png)
<br>

수정 페이지에서 다시 목록 페이지로 이동할 때 검색 조건을 유지하도록 수정합니다.<br>

# 20. 
---
<br>

![20](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/20.png)
<br>

조회 페이지로 리다이렉트 할 때 검색 조건을 유지하도록 GuestbookController의 addAttribute 목록에 type, keyword를 추가합니다.

# 21. 
---
<br>

![21](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/21.png)
<br>

# 21. 
---
<br>

![22](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/22.png)
<br>

# 21. 
---
<br>

![23](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/23.png)
<br>

수정 페이지에서 조회 페이지와 목록 페이지로 이동할 때 검색 조건이 정상적으로 유지되는 것을 확인할 수 있습니다.<br>