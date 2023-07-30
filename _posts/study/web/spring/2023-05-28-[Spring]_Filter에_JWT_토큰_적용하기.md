---
layout: post
title: "[Spring] Filter에 JWT 토큰 적용하기"
subtitle: Spring
date: '2023-05-28 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>



---
<br>

# 1. SecurityConfig - wtiUtil() 생성
---
<br>

![1](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/1.png)
<br>



# 2. ApiLoginFilter - jwtUtil 추가
---
<br>

![2](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/2.png)
<br>




# 3. ApiLoginFilter - successfulAuthentication() 수정
---
<br>

![3](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/3.png)
<br>



# 4. ApiLoginFilter - jwtUtil 추가 결과
---
<br>

![4](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/4.png)
<br>




# 5. ApiCheckFilter - jwtUtil 추가
---
<br>

![5](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/5m.png)
<br>



# 6. ApiCheckFilter - checkAuthHeader() 수정
---
<br>

![6](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/6m.png)
<br>



# 7. SecuriyConfig - apiCheckFilter() 수정
---
<br>

![7](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/e.png)
<br>



# 8. YARC - JWT Header 추가 request
---
<br>

![8](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/8.png)
<br>




# 9. YARC - JWT Header 추가 request 결과
---
<br>

![9](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/9.png)
<br>



# 10. YARC - JWT Header 제거 request 결과
---
<br>

![10](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/10.png)
<br>



# 11. CORSFilter 생성
---
<br>

![11](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/11.png)
<br>


