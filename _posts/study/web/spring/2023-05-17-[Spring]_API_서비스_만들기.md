---
layout: post
title: "[Spring] API 서비스 만들기"
subtitle: Spring
date: '2023-05-17 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

JSON을 이용하는 API 서버를 만들어봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

최근의 서버는 XML이나 JSON 데이터를 전송하는 역할이 점점 커지고 있습니다. 이처럼 클라이언트가 원하는 데이터를 제공하는 서버를 API 서버라고 합니다.<br>
API 서버를 구성할 떄 보안과 인증은 중요한 부분입니다. 이를 스프링 시큐리티와 JWT(JSON Web Token)을 사용해 처리합니다.<br>
간단하게 Note 엔티티를 생성한 뒤 이를 사용하는 예제를 구성합니다.<br>

---
<br>

# 1. Note 생성
---
<br>

![1](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/1.png)
<br>

프로젝트의 entity 패키지에 Note 엔티티를 위의 그림과 같이 작성합니다.<br>
writer는 ClubMember와 `@ManyToOne`의 관계로 구성합니다.<br>
엔티티를 수정할 수 있도록 하는 changeTitle()과 changeContent()를 작성합니다.<br>

# 2. NoteRepository 생성
---
<br>

![2](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/2.png)
<br>

Note에 대한 JPA 처리를 위해 NoteRepository를 작성합니다.<br>
Note의 num을 사용해 찾아 작성자의 정보와 함께 가져오는 getWithWriter()와 작성자의 email을 사용해 작성한 Note들을 불러오는 getList()를 작성합니다.<br>
작성자에 대한 처리를 `@EntityGraph`를 사용해 writer의 로딩 설정을 변경합니다. writer는 ClubMember와 연관관계를 맺고 있었습니다.<br>

# 3. NoteDTO 생성
---
<br>

![3](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/3.png)
<br>

Note 엔티티를 다루기 위해 NoteDTO를 구성합니다.<br>
dto 패키지를 생성하고 NoteDTO를 위와 같이 작성합니다.<br>


# 4. NoteService 생성
---
<br>

![4](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/4.png)
<br>

service 패키지를 추가한 뒤 NoteService를 생성합니다.<br>
NoteService에는 CRUD를 위한 메소드와 dtoToEntity(), entityToDTO()를 작성합니다.<br>


# 5. NoteServiceImpl 생성 1
---
<br>

![5](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/5.png)
<br>

NoteServiceImpl에서는 NoteRepository를 주입받은 뒤 NoteService에서 선언해둔 메소드들을 구현합니다.<br>
우선 register()와 read()를 구현합니다. register()는 save()를 사용하고 read()의 경우 NoteRepository에서 작성한 getWithWriter()를 사용합니다.<br>

# 6. NoteServiceImpl 생성 2
---
<br>

![6](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/6.png)
<br>

modify()와 remove(), getAllWithWriter()를 구현합니다. modify()의 경우 엔티티 클래스에서 작성한 changeTitle()과 changeContent()를 사용하고. getAllWithWriter()는 NoteRepository에서 작성한 getList()를 사용합니다.<br>

# 7. NoteTest 생성 및 결과 
---
<br>

![7](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/8.png)
<br>

간단하게 작성했던 기능들을 테스트합니다.<br>

# 8. NoteController - register() 작성
---
<br>

![8](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/7.png)
<br>

엔티티, DTO, 서비스 계층을 작성했으니 컨트롤러 계층을 작성합니다. JSON으로 데이터를 처리하는 NoteController는 `@RestController`를 사용해 구현합니다.<br>
controller 패키지를 생성한 뒤 NoteController를 생성하고 먼저 register()를 작성합니다.<br>
register()는 POST 방식으로 새로은 Note를 등록할 수 있도록 합니다. `@RequestBody`를 이용해 JSON 데이터를 받은 뒤 NoteDTO로 변환 후 저장합니다.<br>


# 9. YARC 다운로드
---
<br>

![9](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/9.png)
<br>

별도의 화면을 구성하지 않고 테스트를 하기 위한 도구인 `Yet Another REST Client`를 사용해 테스트해봅니다.<br>


# 10. YARC - register() request 
---
<br>

![10](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/10.png)
<br>

먼저 register()에 대한 REST 테스트를 진행합니다.<br>
테스트를 할 때 주의할 점은 반드시 데이터베이스에 존재하는 ClubMember의 메일 계정을 사용해야 한다는 점입니다.<br>
Request Settings에 컨트롤러에서 작성한 URL을 적습니다. POST 방식으로 Payload에 JSON 타입의 데이터를 작성한 뒤 오른쪽 하단의 Send Request 버튼을 클릭합니다.<br>


# 11. YARC - register() request 결과
---
<br>

![11](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/11.png)
<br>

실행 결과 정상적으로 200이 출력되고 작성된 Note의 num을 확인할 수 있습니다.<br>


# 12. NoteController - read() 작성
---
<br>

![12](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/12.png)
<br>

다음으로 read()를 작성합니다.<br>
read()의 경우 GET 방식으로 동작하며 'note/3'과 같이 URL을 작성할 경우 3번 Note를 불러올 수 있게 `@PathVariable`을 사용해 Note의 num을 얻도록 작성합니다.<br>


# 13. YARC - read() request 결과
---
<br>

![13](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/13.png)
<br>

read()의 경우 별도의 Payload 없이 URL만 작성 후 GET 방식으로 Send Request 결과 그림과 같이 테스트로 등록한 Note를 확인할 수 있습니다.<br>


# 14. NoteController - getList() 작성
---
<br>

![14](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/14.png)
<br>

이메일을 사용해 해당 회원이 작성한 모든 글을 불러오는 getList()를 작성합니다.<br>
GET 방식으로 동작하며 파라미터로 전달되는 이메일 주소를 통해 해당 회원이 작성한 Note를 JSON으로 반환합니다.<br>

# 15. YARC - getList() request 결과
---
<br>

![15](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/15.png)
<br>

URL에 이메일을 작성한 뒤 GET 방식으로 Send Request결과 정상적으로 작성한 Note들이 불러와지는 것을 확인할 수 있습니다.<br>

# 16. NoteController - remove() 작성
---
<br>

![16](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/16.png)
<br>

remove()의 경우 DELETE 방식으로 처리합니다.<br>
`@PathVariable`을 사용해 해당 번호를 remove()의 파라미터로 사용해 삭제하도록 작성합니다.<br>

# 17. YARC - remove() request 결과
---
<br>

![17](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/17.png)
<br>

URL을 작성한 뒤 DELETE 방식으로 Send Request 결과 정상적으로 삭제처리된 뒤 removed가 반환되는 것을 확인할 수 있습니다.<br>

# 18. NoteController - modify() 작성
---
<br>

![18](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/18.png)
<br>

마지막으로 수정을 위한 modify()를 작성합니다.<br>
register()와 같이 `@RequestBody`를 사용하지만 PUT 방식으로 처리합니다.<br>

# 19. YARC - modify() request 결과
---
<br>

![19](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/19.png)
<br>

등록할 때와는 달리 Payload에 num값을 같이 전송합니다. PUT 방식으로 Send Request 결과 정상적으로 수정된 것을 확인할 수 있습니다.<br>
