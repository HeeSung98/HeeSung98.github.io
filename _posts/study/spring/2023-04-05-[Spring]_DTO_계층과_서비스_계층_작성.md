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

# 6. list 화면을 위한 목록 처리
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
fn과 result를 pageRequestDTO에 담은 뒤 반환합니다.

# 9. BoardServiceTests testList() 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/9.png)
<br>

BoardService의 getList()의 동작 여부를 테스트하는 테스트 코드를 작성합니다.<br>
BoardServiceTests에 testList()를 위의 그림과 같이 작성합니다.<br>

# 10. 검색 결과 확인
---
<br>

![10](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/10.png)
<br>

짤린 부분의 내용은 BoardDTO(bno=101, title=Test, content=register test, writerEmail=user100@testmail.com, writerName=USER100, regDate=2023-04-06T16:14:51, modDate=2023-04-06T16:14:51, replyCount=0) 입니다.<br>

# 11. 초기화 결과 확인
---
<br>

![11](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/11.png)
<br>

브라우저에서 Clear 버튼을 누른 결과 모든 조건이 지워진 뒤 1페이지로 이동하는 것을 확인할 수 있습니다.<br>

# 12. list.html 페이지 번호 검색 조건 추가
---
<br>

![12](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/12.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 후 나온 결과들의 페이지 번호를 출력하도록 코드를 작성합니다.<br>
기존의 하단 페이지 번호의 링크 '/guestbook/list(page = ...)'으로 처리된 부분에 type과 keyword를 추가합니다.


# 13. gno 링크 검색 조건 추가
---
<br>

![13](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/13.png)
<br>

gno를 눌러 read 페이지로 가는 것 또한 12번과 같이 type과 keyword를 추가해 처리합니다.<br>

# 14. 페이지 번호 검색 조건 추가 결과
---
<br>

![14](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/14.png)
<br>

목록 페이지 하단의 페이지 번호가 검색 결과를 반영하는지 확인합니다.<br>
글 제목에 10이 들어간 방명록을 조회한 뒤 2번 페이지로 이동한 결과 정상적으로 페이지의 이동에 type과 keyword가 반영된 것을 확인할 수 있습니다.

# 15. gno 링크 검색 조건 추가 결과
---
<br>

![15](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/15.png)
<br>

gno 링크를 통한 read 페이지 이동이 검색 조건을 반영하는지 확인합니다.<br>
제목에 wow를 검색한 뒤 read 페이지로 이동한 결과 정상적으로 type과 keyword가 반영된 것을 확인할 수 있습니다.

# 16. read.html 검색 조건 추가
---
<br>

![16](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/16.png)
<br>

조회 페이지에서 목록 페이지로 돌아갈 때 또한 검색 조건을 유지하도록 추가합니다.<br>
read.html의 Modify와 ToList 버튼에 type과 keyword를 넘기도록 작성합니다.<br>

# 17. read.html 검색 조건 추가 결과
---
<br>

![17](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/17.png)
<br>

Modify와 ToList버튼의 링크를 브라우저의 개발자 도구를 통해 확인한 결과 정상적으로 링크가 적용된 것을 확인할 수 있습니다.

# 18. modify.html 검색 조건 추가 - 1
---
<br>

![18](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/18.png)
<br>

수정 페이지 또한 조회 페이지로 이동할 때 검색 조건을 유지하도록 수정합니다.<br>

# 19. modify.html 검색 조건 추가 - 2
---
<br>

![19](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/19.png)
<br>

수정 페이지에서 다시 목록 페이지로 이동할 때 검색 조건을 유지하도록 수정합니다.<br>

# 20. GuestbookController 수정
---
<br>

![20](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/20.png)
<br>

조회 페이지로 리다이렉트 할 때 검색 조건을 유지하도록 GuestbookController의 addAttribute 목록에 type, keyword를 추가합니다.

# 21. 수정 페이지 검색 조건 추가 결과
---
<br>

![21](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/21.png)
<br>
<br>

![22](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/22.png)
<br>
<br>

![23](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/23.png)
<br>

수정 페이지에서 조회 페이지와 목록 페이지로 이동할 때 검색 조건이 정상적으로 유지되는 것을 확인할 수 있습니다.<br>