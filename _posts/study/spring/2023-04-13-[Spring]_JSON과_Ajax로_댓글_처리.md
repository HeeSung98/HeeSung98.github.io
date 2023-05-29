---
layout: post
title: "[Spring] JSON과 Ajax로 댓글 처리"
subtitle: Spring
date: '2023-04-14 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

JSON과 Ajax로 댓글 처리를 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
게시물의 조회 하면에서 댓글을 처리할 수 있도록 합니다.<br>
REST 방식이라고 불리는 다양한 방식의 호출을 이용해 댓글을 처리합니다.<br>
Ajax를 이용해 컨트롤러와 JSON 포맷으로 데이터를 교환하는 방식을 사용합니다.<br>

---
<br>

# 1. Reply - Board와의 연관관계 추가
---
<br>

![1](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/1.png)
<br>

Reply 엔티티가 Board와의 다대일 연관관계를 갖도록 수정합니다.<br>
Board는 toString()시에 제외되도록 하고, LAZY 로딩으로 설정합니다.<br>

# 2. ReplyRepository - getRepliesByBoardOrderByRno() 추가 
---
<br>

![2](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/2.png)
<br>

ReplyRepository 인터페이스에 Board 객체를 파라미터로 받고 모든 댓글을 순번대로 가져오는 getRepliesByBoardOrderByRno()를 작성합니다.<br>


# 3. ReplyRepositoryTests - testListByBoard() 작성 및 결과
---
<br>

![3](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/3.png)
<br>

getRepliesByBoardOrderByRno를 테스트하기 위한 testListByBoard()를 작성합니다.<br>
97번 게시글에 달린 댓글을이 정상적으로 출력되는지 실행 결과를 살펴봅니다.<br>
테스트 수행 결과 97번 게시글에 달린 15번 댓글과 98번 댓글이 정상적으로 출력되는 것을 확인할 수 있습니다.

# 4. ReplyDTO 작성
---
<br>

![4](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/4.png)
<br>

Reply를 컨트롤러와 서비스 영역에서 처리하기 위한 ReplyDTO 클래스를 추가합니다.<br>
ReplyDTO는 Reply 엔티티와 유사하지만 게시물의 번호만을 가지는 형태로 작성합니다.<br>

# 5. ReplyService 작성
---
<br>

![5](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/5.png)
<br>

ReplyService 인터페이스에서는 ReplyDTO를 Reply 엔티티로 처리하거나 반대의 경우에 대한 처리를 작성합니다. 또한 댓글을 등록하는 기능, 특정 게시물의 댓글 리스트를 가져오는 기능, 댓글을 수정하고 삭제하는 기능을 선언합니다.<br>
이 때 dtoToEntity()의 경우 Relpy 엔티티 객체가 Board 엔티티 객체를 참조하기 때문에 Board 객체의 처리가 필요합니다.<br>

# 6. ReplyServiceImpl 작성
---
<br>

![6](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/6.png)
<br>

앞서 ReplyService 인터페이스에 선언한 기능들을 구현합니다.<br>
ReplyDTO를 Reply 엔티티로 저장한 뒤 해당 댓글의 rno를 반환하는 register(), getRepliesByBoardOrderByRno를 통해 Reply 엔티티 List를 받아온 뒤 이를 하나씩 ReplyDTO로 변환한 후 DTO 리스트를 반환하는 getList(), 댓글을 수정하고 삭제하는 modify()와 remove()를 작성합니다.<br> 

# 7. ReplyServiceTests testGetList() 작성 및 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/7.png)
<br>

작성한 getList()기능의 테스트를 위해 ReplyServiceTests 클래스를 생성한 뒤 testGetList()ㄹ를 작성합니다.<br>
ReplyService를 주입한 뒤 getList()를 수행한 후 해당 결과를 ReplyDTO 리스트에 담은 뒤 하나씩 출력합니다.<br>
실행 결과 100번 게시글에 대한 댓글들의 DTO들이 정상적으로 출력되는 것을 확인할 수 있습니다.<br>

# 8. ReplyController 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/8.png)
<br>

서비스 계층까지 완료됐다면 컨트롤러를 만들어 조회 화면에서 댓글을 표시해야 합니다.<br>
@RestController를 이용해 댓글 데이터를 JSON으로 만들어 처리하도록 합니다. @RestController의 모든 메소드는 JSON을 리턴 타입으로 사용합니다.<br>
다음으로 @GetMapping()을 이용해 URL의 일부를 '{}'로 묶은 변수로 사용하는데 이는 메소드 내에서 @PathVariable을 사용해 처리할 수 있습니다. 즉, 'replies/board/100'과 같이 게시물 번호로 조회할 때 100은 '{bno}'로 처리되고 이를 @PathVariable("bno")로 가져와 메소드에서 변수로 사용할 수 있게 됩니다.<br>


# 9. 브라우저에서 게시물 번호 조회
---
<br>

![9](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/9.png)
<br>

이제 프로젝트를 실행한 뒤 브라우저에서 특정 게시물 번호로 조회한다면 위의 그림과 같은 결과를 확인할 수 있습니다.<br>
100번 게시글의 댓글들이 JSON 타입으로 보여지고 있는 것을 확인할 수 있습니다.<br>

# 10. read.html - Reply Count 버튼 추가
---
<br>

![10](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/10.png)
<br>

이제 조회 화면에서 댓글을 볼 수 있도록 합니다.<br>
조회 화면에서는 사용자가 해당 게시물의 댓글 수를 파악한 뒤 댓글의 숫자를 클릭하면 Ajax로 데이터를 처리해 댓글이 보여지도록 작성하고자 합니다.<br>
이를 위해 먼저 게시물의 댓글 수를 보여주는 부분을 작성합니다.<br>

# 11. read.html - Reply Count 버튼 추가 결과
---
<br>

![11](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/11.png)
<br>

브라우저에서 확인하면 위의 그림과 같이 Reply Count 3 이라는 버튼이 생긴것을 확인할 수 있습니다.<br>

# 12. read.html - Reply Count 스크립트 추가
---
<br>

![12](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/12.png)
<br>

Reply Count 버튼을 클릭할 때 발생하는 이벤트 처리를 \<script\> 태그를 작성해 처리합니다.<br>
Reply Count를 클릭할 때 해당 게시물의 댓글을 jquery의 getJSON()을 활용해 가져오고 console.log()를 이용해 확인할 수 있도록 작성합니다.

# 13. read.html - Reply Count 스크립트 추가 결과
---
<br>

![13](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/13.png)
<br>

브라우저에서 Reply Count 버튼을 누른 결과를 개발자 도구의 콘솔창에서 확인해보면 정상적으로 댓글들이 JSON 타입으로 가져와지는 것을 알 수 있습니다.<br>

# 14. read.html - 댓글 조회 기능 추가
---
<br>

![14](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/14m.png)
<br>

댓글 조회 기능은 새로운 댓글이 추가되는 상황이나 댓글의 수정, 삭제 시에도 동작할 필요가 있기 때문에 별도의 함수로 분리해 작성합니다.<br>
formatTime()은 날짜 처리를 위한 함수이고 loadJSONData()는 특정 게시글의 댓글을 처리하는 함수입니다.<br>
loadJSONData()는 Ajax를 이용해 가져온 JSON 데이터를 통해 화면상의 댓글 숫자를 갱신해 주고, 화면에 필요한 태그로 만들어 댓글 목록을 담당하는 \<div\>에 내용으로 추가합니다.

# 15. read.html - 댓글 조회 기능 추가 결과
---
<br>

![15](/assets/img/study_Web/spring/2023-04-13-[Spring]_JSON과_Ajax로_댓글_처리/15.png)
<br>

브라우저에서 Reply Count 버튼을 누른 결과 정상적으로 댓글들이 보여지는 것을 확인할 수 있습니다.<br>