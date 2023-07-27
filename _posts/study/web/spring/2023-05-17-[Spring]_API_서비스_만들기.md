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
Note는 ClubMember와 `@ManyToOne`의 관계로 구성합니다.<br>
엔티티를 수정할 수 있도록 하는 changeTitle()과 changeContent()를 작성합니다.<br>

# 2. NoteRepository 생성
---
<br>

![2](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/2.png)
<br>

Note에 대한 JPA 처리를 위해 NoteRepository를 작성합니다.<br>
Note의 num을 사용해 찾아 작성자의 정보와 함께 가져오는 getWithWriter()와 작성자의 email을 사용해 작성한 Note들을 불러오는 getList()를 작성합니다.<br>
작성자에 대한 처리를

# 3. 
---
<br>

![3](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/3.png)
<br>



# 4. 
---
<br>

![4](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/4.png)
<br>




# 5. 
---
<br>

![5](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/5.png)
<br>



# 6. 
---
<br>

![6](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/6.png)
<br>



# 7. 
---
<br>

![7](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/7.png)
<br>



# 8. 
---
<br>

![8](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/8.png)
<br>




# 9. 
---
<br>

![9](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/9.png)
<br>



# 10. 
---
<br>

![10](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/10.png)
<br>



# 11. 
---
<br>

![11](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/11.png)
<br>



# 12. 
---
<br>

![12](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/12.png)
<br>



# 13. 
---
<br>

![13](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/13.png)
<br>



# 14. 
---
<br>

![14](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/14.png)
<br>



# 15. 
---
<br>

![15](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/15.png)
<br>



# 16. 
---
<br>

![16](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/16.png)
<br>



# 17. 
---
<br>

![17](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/17.png)
<br>



# 18. 
---
<br>

![18](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/18.png)
<br>



# 19. 
---
<br>

![19](/assets/img/web/spring/2023-05-17-[Spring]_API_서비스_만들기/19.png)
<br>


