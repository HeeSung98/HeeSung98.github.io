---
layout: post
title: "[Spring] board 엔티티 테스트"
subtitle: Spring
date: '2023-04-01 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
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

# 1. MemberRepositoryTest insertMembers() 작성
---
<br>

![1](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/1.png)
<br>

test 폴더에서 위의 그림과 같은 경로에 repository 패키지를 작성한 뒤 각각 엔티티마다 RepositoryTest 클래스를 작성합니다.<br>
먼저 MemberRepositoryTest에 예제로 사용할 Member 객체를 100개 추가하는 코드를 위의 그림과 같이 작성합니다.<br>

# 2. MemberRepositoryTest insertMembers() 테스트 결과
---
<br>

![2](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/2.png)
<br>

테스트 실행 결과 데이터베이스에 회원 데이터가 100개 추가된 것을 확인할 수 있습니다.<br>


# 3. BoardRepositoryTest insertBoard() 작성
---
<br>

![3](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/3.png)
<br>

BoardRepositoryTest 또한 동일한 경로에 작성한 뒤 Board 객체를 이용해 생성하도록 코드를 작성합니다. insertBoard()는 한 명의 사용자가 하나의 게시글을 등록하도록 작성됐습니다.<br>
주의할 점은 앞서 작성한 member의 email과 동일하도록 작성해야 하는 점입니다.<br>


# 4. BoardRepositoryTest insertBoard() 테스트 결과
---
<br>

![4](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/4.png)
<br>

테스트 실행 결과 데이터베이스에 보드 데이터가 100개 추가된 것을 확인할 수 있습니다.<br>

# 5. ReplyRepositoryTest insertReply() 작성
---
<br>

![5](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/5.png)
<br>

ReplyRepository 역시 동일한 경로에 작성한 뒤 임의의 게시글에 댓글이 달리도록 위의 그림과 같이 코드를 작성합니다.<br>
1번에서 100번 게시글에 댓글이 달리는데 게시글의 bno를 잘 확인해 번호를 일치시킨 후 댓글이 추가되도록 작성합니다.<br>

# 6. ReplyRepositoryTest insertReply() 테스트 결과
---
<br>

![6](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/6.png)
<br>

테스트 실행 결과를 데이터베이스로 살펴봅니다.<br>
board_bno를 기준으로 정렬해본 결과 위의 그림과 같이 게시글별로 댓글이 작성된 것을 확인할 수 있습니다. 이러한 댓글은 랜덤을 통해 생성했기 때문에 환경마다 다른 결과가 나오게 될 것입니다.<br>
제 board의 100번 게시글에는 댓글이 3개 달린 것을 확인할 수 있습니다.<br>

# 7. BoardRepositorytest testRead1() 작성
---
<br>

![7](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/7.png)
<br>

현재 존재하는 데이터를 화면에 출력할 때 목록 화면에는 bno, title, writer, email과 board에 달린 reply의 개수가 출력됩니다.<br>
엔티티의 작성과 생성을 확인했으니 이제 Board를 조회하는 테스트 코드를 작성합니다.<br>
Repository의 findById를 사용해 100번 게시글을 가져와 조회합니다.<br>

# 8. BoardRepositorytest testRead1() 테스트 결과
---
<br>

![8](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/8.png)
<br>

테스트의 결과를 살펴보면 left outer join을 사용해 결과를 가져오는 것을 확인할 수 있습니다.<br>


# 9. ReplyRepositorytest readReply1() 작성
---
<br>

![9](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/9.png)
<br>

Reply 또한 findById를 사용해 1번 댓글을 조회하도록 테스트 코드를 작성합니다.<br>

# 10. ReplyRepositorytest readReply1() 테스트 결과
---
<br>

![10](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/10.png)
<br>

테스트 결과 Reply 또한 left outer join을 사용해 가져오는 것을 확인할 수 있습니다.<br>
이때 실행된 쿼리문을 보면 reply 테이블 board 테이블 meber 테이블을 모두 조인해 가져옵니다. Reply를 가져올 때마다 Board와 Member까지 가져온다면 굉장히 비효율적일 것입니다.<br>

# 11. Eager loading과 Lazy loading
---
<br>

![11](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/11.png)
<br>

JPA에서 연관관계의 데이터를 어떻게 가져오는가를 `fetch`라고 하는데 @ManyToOne 어노테이션의 속성으로 fetch 모드를 결정합니다.<br>
10번의 테스트 결과와 같이 모든 연관관계의 엔티티를 같이 가져오는 것을 `Eager loading`(즉시 로딩)이라고 합니다. Eager loading은 한번에 모든 엔티티를 가져오는 장점이 잇지만 성능 저하를 피할 수 없는 단점이 있습니다. 때문에 Eager loading의 반대 개념인 `Lazy loading`(지연 로딩)을 사용해 처리하도록 합니다.<br>
위의 코드와 같이 fetchType을 Lazy로 설정합니다.<br>

# 12. ReplyRepositorytest readReply1() Lazy Loading 테스트 결과
---
<br>

![12](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/12.png)
<br>

fetch mode를 Lazy로 지정한 뒤 테스트 코드를 다시 실행해보면 proxy - no session 예외가 발생하는 것을 확인할 수 있습니다.<br>
지연 로딩 방식으로 데이터를 가져오기 때문에 board 테이블만을 가져온 뒤 데이터베이스와의 연결은 끝나게 됩니다. 때문에 board.getWirter()를 실행할 때 member 테이블을 로딩할 수 없기 때문에 생긴 문제입니다.<br>



# 13. ReplyRepositorytest @Transactional readReply1() Lazy Loading 테스트 결과
---
<br>

![13](/assets/img/web/spring/2023-04-01-[Spring]_board_엔티티_테스트/13.png)
<br>

12번에서 발생한 것과 같은 문제를 해결하기 위해 메소드에 `@Transactional` 어노테이션을 추가합니다. @Transactional을 통해 메소드가 하나의 트랜잭션으로 처리돼 board.getWriter()를 실행할 때 다시 데이터베이스와 연결되도록 합니다.<br>
@Transactional을 작성한 뒤 readReply1()을 실행한 결과 board 테이블만을 로딩해 사용한 뒤 board.getWirter()를 처리하기 위해 member 테이블을 로딩합니다. 즉시 로딩에서 board 테이블과 member 테이블을 조인해 처리한 것과는 차이가 있음을 확인할 수 있습니다.<br><br>

앞서 엔티티를 생성할 때 연관관계를 사용하는 엔티티의 @ToString 속성에 exclude를 추가했었습니다. Board 객체의 멤버 변수를 출력할 때 Member 객체 또한 모두 출력되어야 하고 데이터베이스의 연결이 필요하게 됩니다. 연관관계 엔티티를 지연로딩 처리한 채 exclude 속성을 지정하지 않고 @ToString이 수행될 경우 연관관계 엔티티를 가져올 때 데이터베이스와의 연결이 끊기게 되어 예외가 생기게 됩니다. 떄문에 연관관계 엔티티에서 @ToString은 주의해 사용해야 합니다.<br>
