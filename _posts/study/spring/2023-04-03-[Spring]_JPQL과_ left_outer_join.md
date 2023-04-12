---
layout: post
title: "[Spring] JPQL과 left outer join"
subtitle: Spring
date: '2023-04-03 14:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

JPQL을 사용해 left outer join을 수행해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
리스트 화면에서 게시글의 정보와 작성자의 정보, 그리고 댓글의 수를 함께 가져올 때 하나의 엔티티만을 사용해 가져올 수는 없습니다. 그렇기 때문에 JPQL의 join을 사용해 가져오는 방법을 수행하려 합니다.<br>

---
<br>

# 1. @Query getBoardWithWriter() 작성
---
<br>

![1](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/1.png)
<br>

Board 엔티티 클래스 내부에는 Member 엔티티 클래스 타입의 멤버 변수 writer가 존재하고 연관관계를 가집니다. 이러한 Board의 writer 변수를 이용해 조인을 수행하도록 getBoardWithWriter()를 작성합니다.<br>
getBoardWithWriter()는 Board를 사용하지만 Member 또한 조회해야 합니다. Board와 Member는 연관관계를 맺고있기 때문에 b.writer의 형태로 작성합니다.<br>

# 2. BoardRepositoryTest testReadWithWriter() 테스트
---
<br>

![2](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/2.png)
<br>

작성한 getboardWitWriter()를 테스트하기 위해 testReadWithWriter()를 작성한 뒤 실행합니다.<br>



# 3. BoardRepositoryTest testReadWithWriter() 테스트 결과
---
<br>

![3](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/3.png)
<br>

실행 결과를 살펴보면 지연 로딩으로 처리했지만 실행되는 커리는 조인 처리돼 한번에 board 테이블과 membe 테이블을 이용하는 것을 알 수 있습니다.<br>
result로 가져온 arr을 살펴보면 0번 인덱스에는 Board의 정보가 담겨있고 1번 인덱스에는 Member의 정보가 담겨있는 것을 확인할 수 있습니다.


# 4. 연관관계가 없을 때의 처리
---
<br>

![4](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/4.png)
<br>

Board와 Member의 경우 내부적인 참조를 통해 연관관계를 가지지만 Board는 Reply를 참조하고 있지 않습니다. Board에 Reply의 개수를 출력해야 하기 때문에 join on을 사용해 작성합니다.<br>
목록으로 가져올 Board에 속한 댓글을 조회하도록 순수한 SQL 쿼리문을 작성할 수 있고 결과는 위의 그림과 같습니다.<br>

# 5. @Query getBoardWithReply() 작성
---
<br>

![5](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/5.png)
<br>

4번에서 작성한 쿼리를 JPQL로 작성한 것은 위의 그림과 같습니다.<br>
join on을 사용해 reply의 board 데이터와 선택할 board 데이터가 같은 것만 조인되도록 작성합니다.<br>

# 6. BoardRepositoryTest testGetWithReply() 테스트
---
<br>

![6](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/6.png)
<br>

getBoardWithReply()를 테스트하기 위한 testGetWithReply()를 위의 그림과 같이 작성합니다.<br>

# 7. BoardRepositoryTest testGetWithReply() 테스트 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/7.png)
<br>

실행 결과는 위의 그림과 같고 testReadWithWriter()의 결과와 같이 0번 인덱스에 Board의 정보가 담겨있고 1번 인덱스의 Reply의 정보가 담겨있는 것을 확인할 수 있습니다.<br>

# 8. @Query getBoardWithReplyCount() 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/8.png)
<br>

list 화면의 구성 요소로<br>
Board의 bno, writer, regDate<br>
Member의 writer, writer_email<br>
Reply의 ReplyCount가 필요했습니다.<br>
Board를 기준으로 조인 관계를 작성해 조인한 뒤 GROUP BY를 통해 하나의 게시물이 한 라인이 되도록 처리하고자 합니다.<br>
화면 출력을 위해 Pageable 타입의 매개변수를 전달받은 뒤 Page\<Object[]\>

# 9. list.html 이벤트 처리 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/9.png)
<br>

앞서 list.html에서 작성한 Search 버튼과 Clear 버튼의 이벤트를 처리하는 코드를 작성합니다.<br>
'btn-search'를 클릭하면 검색 타입과 키워드로 1페이지를 검색하도록 작성하고 'btn-clear'를 클릭하면 모든 검색 내용을 삭제한 뒤 목록 페이지로 이동하도록 작성합니다.<br>

# 10. 검색 결과 확인
---
<br>

![10](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/10.png)
<br>

브라우저에서 조건을 입력한 뒤 Search 버튼을 누른 결과 정상적으로 검색이 되는 것을 확인할 수 있습니다.<br>

# 11. 초기화 결과 확인
---
<br>

![11](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/11.png)
<br>

브라우저에서 Clear 버튼을 누른 결과 모든 조건이 지워진 뒤 1페이지로 이동하는 것을 확인할 수 있습니다.<br>

# 12. list.html 페이지 번호 검색 조건 추가
---
<br>

![12](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/12.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 후 나온 결과들의 페이지 번호를 출력하도록 코드를 작성합니다.<br>
기존의 하단 페이지 번호의 링크 '/guestbook/list(page = ...)'으로 처리된 부분에 type과 keyword를 추가합니다.


# 13. gno 링크 검색 조건 추가
---
<br>

![13](/assets/img/study_Web/spring/2023-04-03-[Spring]_JPQL과_ left_outer_join/13.png)
<br>

gno를 눌러 read 페이지로 가는 것 또한 12번과 같이 type과 keyword를 추가해 처리합니다.<br>
