---
layout: post
title: "[Spring] 스프링 시큐리티 프로젝트를 위한 JPA 처리"
subtitle: Spring
date: '2023-05-10 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

프로젝트에 스프링 시큐리티를 적용하기 위해서는 당연히 이에 맞는 데이터베이스 관련 처리가 필요합니다.<br>
이번 프로젝트는 아이디 대신 이메일을 아이디로 사용해 회원을 처리합니다.<br>
회원 정보는 이메일, 패스워드, 이름, 소셜 회원 가입 여부, 등록일 및 수정일로 구성합니다.<br>
또한 앞서 사용한 권한에 대한 처리 또한 작성합니다.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>



---
<br>

# 1. ClubMember 생성
---
<br>

![1](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/1.png)
<br>



# 2. ClubApplication - @EnableJpaAuditing 작성
---
<br>

![2](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/2.png)
<br>




# 3. ClubMemberRole 생성
---
<br>

![3](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/3.png)
<br>



# 4. ClubMember - addMemberRole() 작성
---
<br>

![4](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/4.png)
<br>



# 5. ER 다이어그램 확인
---
<br>

![5](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/5.png)
<br>



# 6. ClubMemberRepository 생성
---
<br>

![6](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/6.png)
<br>



# 7. ClubMemberTests 생성 및 ClubMemberTests - insertDummies() 작성
---
<br>

![7](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/7.png)
<br>



# 8. ClubMemberTests - insertDummies() 결과
---
<br>

![8](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/8.png)
<br>




# 9. ClubMemberRepository - findByEmail() 작성
---
<br>

![9](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/9.png)
<br>



# 10. ClubMemberTests - testRead() 작성 및 결과
---
<br>

![10](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/10.png)
<br>



# 11. ClubAuthMemberDTO 생성
---
<br>

![11](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/11.png)
<br>



# 12. ClubUserDetailsService 생성
---
<br>

![12](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/12.png)
<br>



# 13. SecurityConfig 생성
---
<br>

![13](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/13.png)
<br>



# 14. ClubUserDetailsService - loadUserByUsername() 작성
---
<br>

![14](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/14.png)
<br>



# 15. ClubUserDetailsService - loadUserByUsername() 결과 1
---
<br>

![15](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/15.png)
<br>



# 16. ClubUserDetailsService - loadUserByUsername() 결과 2
---
<br>

![16](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/16.png)
<br>



# 17. 
---
<br>

![17](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/17.png)
<br>



# 18. 
---
<br>

![18](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/18.png)
<br>



# 19. 
---
<br>

![19](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/19.png)
<br>




