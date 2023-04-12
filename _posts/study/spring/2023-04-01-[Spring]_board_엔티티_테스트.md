---
layout: post
title: "[Spring] board 엔티티 테스트"
subtitle: Spring
date: '2023-04-01 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

작성한 엔티티를 테스트해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
앞서 작성한 3개의 엔티티에 대한 테스트를 수행합니다.<br>
3개의 테이블이 PK와 FK의 관계로 이루어져 있습니다. PK부터 하나씩 테스트코드를 통한 테스트를 해보겠습니다.

---
<br>

# 1. MemberRepositoryTest insertMembers() 테스트
---
<br>

![1](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/1.png)
<br>

test 폴더에서 위의 그림과 같은 경로에 repository 패키지를 작성한 뒤 각각 엔티티마다 RepositoryTest 클래스를 작성합니다.<br>
먼저 MemberRepositoryTest에 예제로 사용할 Member 객체를 100개 추가하는 코드를 위의 그림과 같이 작성합니다.<br>

# 2. MemberRepositoryTest insertMembers() 테스트 결과
---
<br>

![2](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/2.png)
<br>

테스트 실행 결과 데이터베이스에 회원 데이터가 100개 추가된 것을 확인할 수 있습니다.<br>


# 3. BoardRepositoryTest insertBoard() 테스트
---
<br>

![3](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/3.png)
<br>

BoardRepositoryTest 또한 동일한 경로에 작성한 뒤 Board 객체를 이용해 생성하도록 코드를 작성합니다. insertBoard()는 한 명의 사용자가 하나의 게시글을 등록하도록 작성됐습니다.<br>
주의할 점은 앞서 작성한 member의 email과 동일하도록 작성해야 하는 점입니다.<br>


# 4. BoardRepositoryTest insertBoard() 테스트 결과
---
<br>

![4](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/4.png)
<br>

테스트 실행 결과 데이터베이스에 보드 데이터가 100개 추가된 것을 확인할 수 있습니다.<br>

# 5. ReplyRepositoryTest insertReply() 테스트
---
<br>

![5](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/5.png)
<br>

ReplyRepository 역시 동일한 경로에 작성한 뒤 임의의 게시글에 댓글이 달리도록 위의 그림과 같이 코드를 작성합니다.<br>
1번에서 100번 게시글에 댓글이 달리는데 게시글의 bno를 잘 확인해 번호를 일치시킨 후 댓글이 추가되도록 작성합니다.<br>

# 6. ReplyRepositoryTest insertReply() 테스트 결과
---
<br>

![6](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/6.png)
<br>

테스트 실행 결과를 데이터베이스로 살펴봅니다.<br>
board_bno를 기준으로 정렬해본 결과 위의 그림과 같이 게시글별로 댓글이 작성된 것을 확인할 수 있습니다. 이러한 댓글은 랜덤을 통해 생성했기 때문에 환경마다 다른 결과가 나오게 될 것입니다.<br>
제 board의 100번 게시글에는 댓글이 3개 달린 것을 확인할 수 있습니다.<br>

# 7. list.html 검색 항목 작성
---
<br>

![7](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/7.png)
<br>

검색 항목을 생성하기 위히 form을 작성합니다.<br>
동일하게 List로 이동하도록 하지만 option과 input을 사용해 type과 keyword가 입력된 채로 출력도록 작성합니다.<br>

# 8. 검색 항목 결과 
---
<br>

![8](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/8.png)
<br>

6번과 동일하게 type과 keyword를 지정한 url을 작성해 살펴보면 option과 input에 작성한 type과 keyword가 적혀있는 것을 확인할 수 있습니다.<br>

# 9. list.html 이벤트 처리 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/9.png)
<br>

앞서 list.html에서 작성한 Search 버튼과 Clear 버튼의 이벤트를 처리하는 코드를 작성합니다.<br>
'btn-search'를 클릭하면 검색 타입과 키워드로 1페이지를 검색하도록 작성하고 'btn-clear'를 클릭하면 모든 검색 내용을 삭제한 뒤 목록 페이지로 이동하도록 작성합니다.<br>

# 10. 검색 결과 확인
---
<br>

![10](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/10.png)
<br>

브라우저에서 조건을 입력한 뒤 Search 버튼을 누른 결과 정상적으로 검색이 되는 것을 확인할 수 있습니다.<br>

# 11. 초기화 결과 확인
---
<br>

![11](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/11.png)
<br>

브라우저에서 Clear 버튼을 누른 결과 모든 조건이 지워진 뒤 1페이지로 이동하는 것을 확인할 수 있습니다.<br>

# 12. list.html 페이지 번호 검색 조건 추가
---
<br>

![12](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/12.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 후 나온 결과들의 페이지 번호를 출력하도록 코드를 작성합니다.<br>
기존의 하단 페이지 번호의 링크 '/guestbook/list(page = ...)'으로 처리된 부분에 type과 keyword를 추가합니다.


# 13. gno 링크 검색 조건 추가
---
<br>

![13](/assets/img/study_Web/spring/2023-04-01-[Spring]_board_엔티티_테스트/13.png)
<br>

gno를 눌러 read 페이지로 가는 것 또한 12번과 같이 type과 keyword를 추가해 처리합니다.<br>
