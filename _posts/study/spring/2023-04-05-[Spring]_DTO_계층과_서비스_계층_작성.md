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
검색 처리는 PageRequestDTO에 type과 keyword를 추가하고 서비스 계층에서 Querydsl을 이용해 수행합니다. 이 때 제목, 내용, 작성자를 각각 t, c, w라고 할 때 't, w, c', 'tw', 'twc'와 같이 검색 항목을 여러개로 선택해 검색할 수 있도록합니다.

---
<br>

# 1. PageRequestDTO 클래스 수정
---
<br>

![1](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/1.png)
<br>

먼저 PageRequestDTO에 조건(type)과 키워드(keyword)를 추가합니다.

# 2. GuestbookServiceImpl 클래스 수정 (getSearch())
---
<br>

![2](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/2.png)
<br>

Querydsl의 BooleanBuilder를 이용해 동적으로 검색 조건이 처리되게 하도록 GuestbookServiceImpl 내에 getSerach() 메소드를 작성합니다.<br>
getSearc()는 매개변수로 PageRequestDTO를 받아와 type가 존재한다면 conditionBuilder를 사용해 각 검색 조건을 or로 연결해 처리합니다. 검색 조건이 없다면 모든 게시글이 나오도록 gn > 0을 조건으로 해 검색하도록 합니다.<br>


# 3. GuestbookServiceImpl 클래스 수정 (getList())
---
<br>

![3](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/3.png)
<br>

이 때 목록을 가져오는 getList()를 수정해야 합니다.<br>
기존의 pageable만 사용해 목록을 가져오는 것이 아닌 getSearch()의 반환값 booleanBuilder를 사용해 검색 조건과 같이 목록을 가져올 수 있도록 수정합니다.<br>


# 4. getSearch() 테스트
---
<br>

![4](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/4.png)
<br>

작성한 getSearch()를 통해 검색 조건이 잘 처리되나 testSearch() 메소드를 작성해 확인합니다.<br>
검색 조건으로 제목과 내용 중 'shg'라는 단어가 포함된다면 결과를 출력하도록 테스트 코드를 작성합니다<br>

# 5. getSearch() 테스트 결과
---
<br>

![5](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/5.png)
<br>

실행 결과를 스텍트레이스를 통해 살펴보면 쿼리문 바깥에 gno > 0과 type과 쿼리문 안쪽에 keyword를 사용한 like문이 and로 처리되는 것을 확인할 수 있습니다.<br>
검색의 결과로 312번 방명록이 검색되었고 검색된 방명록이 하나이기 때문에 목록의 Prev와 Next가 존재하지 않는 것을 알 수 있습니다.<br>

# 6. 브라우저로 getSearch() 결과
---
<br>

![6](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/6.png)
<br>

브라우저에 type과 keyword를 지정한 url을 작성해 살펴보면 정상적으로 게시글이 검색되는 것을 확인할 수 있습니다.<br>

# 7. list.html 검색 항목 작성
---
<br>

![7](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/7.png)
<br>

검색 항목을 생성하기 위히 form을 작성합니다.<br>
동일하게 List로 이동하도록 하지만 option과 input을 사용해 type과 keyword가 입력된 채로 출력도록 작성합니다.<br>

# 8. 검색 항목 결과 
---
<br>

![8](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/8.png)
<br>

6번과 동일하게 type과 keyword를 지정한 url을 작성해 살펴보면 option과 input에 작성한 type과 keyword가 적혀있는 것을 확인할 수 있습니다.<br>

# 9. list.html 이벤트 처리 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-04-05-[Spring]_DTO_계층과_서비스_계층_작성/9.png)
<br>

앞서 list.html에서 작성한 Search 버튼과 Clear 버튼의 이벤트를 처리하는 코드를 작성합니다.<br>
'btn-search'를 클릭하면 검색 타입과 키워드로 1페이지를 검색하도록 작성하고 'btn-clear'를 클릭하면 모든 검색 내용을 삭제한 뒤 목록 페이지로 이동하도록 작성합니다.<br>

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