---
layout: post
title: "[Spring] JWT 생성 및 검증"
subtitle: Spring
date: '2023-05-25 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

JWT를 발급하고 API에 적용해봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>



---
<br>

# 1. JWT 사이트를 이용한 검증
---
<br>

![1](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/1.png)
<br>



# 2. build.gradle - jjwt 라이브러리 추가
---
<br>

![2](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/2.png)
<br>




# 3. JWTUtil 생성
---
<br>

![3](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/3.png)
<br>



# 4. JWTUtil - validateAndExtract()
---
<br>

![4](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/4.png)
<br>




# 5. JWTTests 생성
---
<br>

![5](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/5.png)
<br>



# 6. JWTTests - testEncode() 결과
---
<br>

![6](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/6.png)
<br>



# 7. testEncode() 결과 검증
---
<br>

![7](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/7.png)
<br>



# 8. JWTTests - testEncode() 수정
---
<br>

![8](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/8.png)
<br>




# 9. JWTTests - testEncode() 수정 결과
---
<br>

![9](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/9.png)
<br>



# 10. JWTUtil - generateToken() 수정
---
<br>

![10](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/10.png)
<br>



# 11. JWTUtil - generateToken() 수정 결과
---
<br>

![11](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/11.png)
<br>


