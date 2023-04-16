---
layout: post
title: "[Spring] DTO 계층과 서비스 계층 작성"
subtitle: Spring
date: '2023-04-05 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

프로젝트의 DTO 계층과 서비스 계층을 작성해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
Board와 Member, Reply 엔티티를 사용하는 테스트가 모두 완료된 상태에서 이제 서비스 계층을 통해 브라우저로 확인할 수 있도록 코드를 작성하고자 합니다.<br>

---
<br>

# 1. BoardDTO 작성
---
<br>

![1](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/1.png)
<br>

먼저 프로젝트 내에 dto, service 패키지를 위의 그림과 같이 생성한 뒤 dto 패키지에 BoardDTO 클래스를 생성합니다.<br>
DTO의 경우 엔티티와는 다르게 참조를 하는 것이 아닌 화면에서 사용되는 정보가 직접 작성되고있는 것을 알 수 있습니다.<br>
Meber와 Reply의 정보인 writerEmail, writerName, replyCount를 모두 작성합니다.<br>

# 2. BoardService dtoToEntity() 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/2.png)
<br>

게시물을 등록할 때 BoardDTO 타입을 매개변수로 받고 생성된 게시물의 번호를 반환하는 dtoToEntity()를 작성합니다.<br>
dtoToEntity()는 Board 엔티티 객체와 Member 엔티티 객체가 연관관계를 가지게 구성해야 합니다. 때문에 Member 엔티티 객체를 생성한 뒤 Board 엔티티 객체에 연관되게 생성합니다.<br>


# 3. BoardService register() 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/3.png)
<br>

dtoToEntity()를 사용해 게시물을 등록하게 하는 register()를 작성합니다.<br>
register()는 BoardDTO를 매개변수로 받아 DTO를 dtoToEntity를 사용해 DTO를 Entity로 변환한 뒤 repository.save()를 사용해 데이터베이스에 저장한 뒤 저장한 Entity의 Bno를 반환합니다.<br>


# 4. BoardServiceTests testRegister() 작성
---
<br>

![4](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/4.png)
<br>

작성한 register()를 테스트할 테스트 코드를 작성합니다. test 폴더에 service 패키지를 추가한 뒤 BoardServiceTests를 생성한 후 tesgRegister()를 작성합니다.<br>
테스트 코드는 위의 그림과 같습니다. 중요한 점은 현재 데이터베이스에 존재하는 회원의 정보로 dto를 만들어야 한다는 것입니다.<br>

# 5. BoardServiceTests testRegister () 결과
---
<br>

![5](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/5.png)
<br>

testRegister() 수행 결과를 데이터베이스에서 살펴본 결과 101번 게시글이 user100@testmail.com의 Member 엔티티를 사용해 정상적으로 등록된 것을 확인할 수 있습니다.<br>

# 6. PageRequestDTO와 PageResultDTO 작성
---
<br>

![6](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/6.png)
<br>

list 화면의 목록을 처리하기 위해서 파라미터를 수집하는 PageRequestDTO와 PageResultDTO를 작성해야 합니다.<br>
두 개의 클래스는 앞서 생성할 때 재사용성을 위해 제너릭을 활용해 작성하였습니다. 때문에 패키지명을 수정하는 것 외에는 별도의 처리 없이 바로 사용할 수 있습니다.<br>

# 7. BoardService entityToDTO() 작성
---
<br>

![7](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/7m.png)
<br>

list 화면에 보여질 DTO를 위해 Entity를 DTO로 변환하는 entityToDTO()를 작성합니다.<br>
PageResultDTO에서 중요한 점은 JPQL의 결과물을 DTO 리스트로 변환하는 기능을 수행한다는 것이였습니다. 이번 board 프로젝트에선 JPQL의 실행 결과로 나오는 Object[]타입을 BoardDTO로 처리해야 합니다.<br>
Object[]는 앞서 테스트 코드에서 살펴본 바 Board, Member, 댓글 수로 구성되어있습니다. 매개변수로 Board와 Member, ReplyCount를 받아오도록 작성합니다. 이 때 replyCount의 경우 long타입에서 int타입으로 캐스팅해 저장하도록 합니다.<br><br>
BoardService에 DTO List를 가져올 getList()를 선언해준 뒤 Impl로 넘어가 구현합니다.<br>

# 8. BoardServiceImpl getList() 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/8.png)
<br>

getList()는 앞서 말한 대로 list 화면에 보여질 DTO인 PageResultDTO를 구성하는 역할 entityToDTO()를 사용해 수행합니다.<br>
getList() 내부에는 Object[]타입을 받아 BoardDTO타입으로 변환하는 Function fn을 작성합니다.<br>
다음으로 작성했던 getBoardWithReplyCount()를 사용해 bno를 기준으로 역순정렬하는 페이지를 Page\<object[]\>타입의 result에 담아옵니다.<br>
fn과 result를 pageRequestDTO에 담은 뒤 반환합니다.<br>

# 9. BoardServiceTests testList() 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/9.png)
<br>

BoardService의 getList()의 동작 여부를 테스트하는 테스트 코드를 작성합니다.<br>
BoardServiceTests에 testList()를 위의 그림과 같이 작성합니다.<br>
pageRequestDTO를 디폴트 생성자로 생성한 뒤 getList의 매개변수로 넘겨준 후 반환값을 result에 담습니다. PageResult는 dtoList를 갖고있으며 이를 하나씩 출력합니다.<br>


# 10. BoardServiceTests testList() 결과
---
<br>

![10](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/10.png)
<br>

실행 결과를 살펴보면 list 화면에 보여질 BoardDTO가 10개 존재하고 있습니다. 위 그림에는 잘렸지만 직접 스크롤을 옮겨 살펴보면 replyCount까지 정상적으로 담겨져 있는 것을 확인할 수 있습니다.<br>

# 11. BoardServiceImpl get() 작성
---
<br>

![11](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/11.png)
<br>

read 화면을 위한 get()을 작성합니다. BoardServiceImpl에 작성하기 전 BoardService에 BoardDTO get()을 선언해둔 상태이며 Impl에 구현 전 인터페이스에 선언해야 하는 것을 놓치지 않길 바랍니다.<br>
getBoardByBno()를 사용해 엔티티를 가져온 뒤 엔티티를 Object[] 타입으로 캐스팅한 후 entityToDTO에 매개변수로 각각 넣어준 뒤 entityToDTO의 결과값을 반환합니다.<br>

# 12. BoardServiceTests testGet() 작성
---
<br>

![12](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/12.png)
<br>

BoardService의 get()의 동작 여부를 테스트하는 테스트 코드를 작성합니다.<br>


# 13. BoardServiceTests testGet() 결과
---
<br>

![13](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/13.png)
<br>

testGet()의 실행 결과는 위의 그림과 같습니다.<br>
정상적으로 100번 게시물의 DTO가 출력되는 것을 확인할 수 있습니다.<br>

# 14. ReplyRepository deleteByBno() 작성
---
<br>

![14](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/14.png)
<br>

게시물의 삭제를 위한 deleteByBno()를 작성합니다.<br>
 게시물을 삭제할 때 게시물의 댓글 또한 같이 삭제해야 합니다. 이를 위해 해당 게시물의 댓글을 모두 삭제한 뒤 게시물을 삭제하는 순서로 처리될 것입니다. 이 때 두 작업은 하나의 Transaction으로 처리해야 합니다.<br>
JPQL을 이용해 update, delete를 수행할 때는 `@Modifying`을 선언해야 합니다.<br>

# 15. BoardService removieWithReplies() 선언
---
<br>

![15](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/15.png)
<br>

BoardService에 게시글 삭제를 위한 removieWithReplies()를 선언합니다.

# 16. BoardServiceImpl removieWithReplies() 작성
---
<br>

![16](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/16.png)
<br>

BoardService에 선언한 removieWithReplies()를 구현합니다.<br>
removieWithReplies()는 ReplyRepository를 주입받아 reply의 엔티티 먼저 삭제한 뒤 board의 엔티티를 삭제합니다. `@Transactional` 어노테이션을 사용해 두 작업이 하나의 Transaction으로 수행되게 합니다.<br>

# 17. BoardServiceTests testRemove() 작성
---
<br>

![17](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/17.png)
<br>

removieWithReplies()를 테스트 하기 위한 testRemove()를 작성합니다.<br>

# 18. BoardServiceTests testRemove() 결과
---
<br>

![18](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/18.png)
<br>

데이터베이스를 살펴본 결과 1번 게시글이 정상적으로 삭제된 것을 확인할 수 있습니다.<br>

# 19. Board changeTitle(), changeContent() 작성
---
<br>

![19](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/19.png)
<br>

게시글의 수정을 위해 Board 엔티티 클래스에 changeTitle(), changeContent()를 작성합니다.<br>
게시글의 수정은 제목과 내용만 수정이 가능하게 하고 제목과 내용을 변경한 뒤 다시 save()하는 방식으로 동작합니다.<br>

# 20. BoardService modify() 선언
---
<br>

![20](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/20.png)
<br>

BoardDTO를 이용해 수정하는 modify()를 선언합니다.<br>

# 21. BoardServiceImpl modify() 작성
---
<br>

![21](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/21.png)
<br>

선언한 modify()를 구현합니다. boardDTO의 Bno를 가져온 뒤 repository.getOne()의 매개변수로 사용합니다. getOne()은 findById()와 다르게 지연 로딩 방식으로 작동됩니다.<br>
가져온 엔티티를 board에 담은 뒤 changeTitle()를 매개변수로 boardDTO의 title을 가져온 뒤 수행하고 ChangeContent를 boardDTO의 content를 가져온 뒤 수행합니다.<br>
그 후 save()를 통해 엔티티를 저장합니다.<br>
<br>

# 21. BoardServiceTests testModify() 작성
---
<br>

![22](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/22.png)
<br>

modify()를 테스트하기 위한 testModify()를 작성합니다.<br>

# 21. BoardServiceTests testModify() 결과
---
<br>

![23](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/23.png)
<br>

데이터베이스를 살펴본 결과 2번 게시물의 제목과 내용이 정상적으로 변경된 것을 확인할 수 있습니다.<br>