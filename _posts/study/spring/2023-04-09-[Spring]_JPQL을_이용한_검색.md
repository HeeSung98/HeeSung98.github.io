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

# 2. 
---
<br>

![2](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/2.png)
<br>

Querydsl의 BooleanBuilder를 이용해 동적으로 검색 조건이 처리되게 하도록 GuestbookServiceImpl 내에 getSerach() 메소드를 작성합니다.<br>
getSearc()는 매개변수로 PageRequestDTO를 받아와 type가 존재한다면 conditionBuilder를 사용해 각 검색 조건을 or로 연결해 처리합니다. 검색 조건이 없다면 모든 게시글이 나오도록 gn > 0을 조건으로 해 검색하도록 합니다.<br>


# 3. 
---
<br>

![3](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/3.png)
<br>

이 때 목록을 가져오는 getList()를 수정해야 합니다.<br>
기존의 pageable만 사용해 목록을 가져오는 것이 아닌 getSearch()의 반환값 booleanBuilder를 사용해 검색 조건과 같이 목록을 가져올 수 있도록 수정합니다.<br>


# 4. 
---
<br>

![4](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/4.png)
<br>

작성한 getSearch()를 통해 검색 조건이 잘 처리되나 testSearch() 메소드를 작성해 확인합니다.<br>
검색 조건으로 제목과 내용 중 'shg'라는 단어가 포함된다면 결과를 출력하도록 테스트 코드를 작성합니다<br>

# 5. 
---
<br>

![5](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/5.png)
<br>

testSearch를 수행할 때 몇 가지 오류를 겪을 수 있습니다. 저는 이러한 오류를 Gradle 설정 변경과 Enable annotation processing 설정, Q클래스 삭제 후 재실행 등을 통해 오류를 해결했습니다. 수행된 결과는 위의 그림과 같으며 log.info를 통해 search1이 수행된 것을 확인할 수 있습니다.

# 6. 
---
<br>

![6](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/6.png)
<br>

브라우저에 type과 keyword를 지정한 url을 작성해 살펴보면 정상적으로 게시글이 검색되는 것을 확인할 수 있습니다.<br>

# 7. 
---
<br>

![7](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/7.png)
<br>

검색 항목을 생성하기 위히 form을 작성합니다.<br>
동일하게 List로 이동하도록 하지만 option과 input을 사용해 type과 keyword가 입력된 채로 출력도록 작성합니다.<br>

# 8. 
---
<br>

![8](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/8.png)
<br>

6번과 동일하게 type과 keyword를 지정한 url을 작성해 살펴보면 option과 input에 작성한 type과 keyword가 적혀있는 것을 확인할 수 있습니다.<br>

# 9. 
---
<br>

![9](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/9.png)
<br>

앞서 list.html에서 작성한 Search 버튼과 Clear 버튼의 이벤트를 처리하는 코드를 작성합니다.<br>
'btn-search'를 클릭하면 검색 타입과 키워드로 1페이지를 검색하도록 작성하고 'btn-clear'를 클릭하면 모든 검색 내용을 삭제한 뒤 목록 페이지로 이동하도록 작성합니다.<br>

# 10. 
---
<br>

![10](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/10.png)
<br>

짤린 부분의 내용은 BoardDTO(bno=101, title=Test, content=register test, writerEmail=user100@testmail.com, writerName=USER100, regDate=2023-04-06T16:14:51, modDate=2023-04-06T16:14:51, replyCount=0) 입니다.<br>

# 11. 
---
<br>

![11](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/11.png)
<br>

브라우저에서 Clear 버튼을 누른 결과 모든 조건이 지워진 뒤 1페이지로 이동하는 것을 확인할 수 있습니다.<br>

# 12. 
---
<br>

![12](/assets/img/study_Web/spring/2023-04-09-[Spring]_JPQL을_이용한_검색/12.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 후 나온 결과들의 페이지 번호를 출력하도록 코드를 작성합니다.<br>
기존의 하단 페이지 번호의 링크 '/guestbook/list(page = ...)'으로 처리된 부분에 type과 keyword를 추가합니다.


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