---
layout: post
title: "[Spring] API 서비스 필터링"
subtitle: Spring
date: '2023-05-18 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

OncePerRequestFilter를 사용해 API 호출 필터링을 살펴봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

API 서비스를 학습하며 사용한 '/notes'는 외부에서 데이터를 주고받기 위한 경로입니다. 이 경로를 외부에서 아무런 제약 없이 호출하는 것은 서버에게 상당한 위험이 될 수 있습니다.<br>
필터를 사용한 필터링을 통해 인증된 사용자에 한해서 서비스를 제공하게 할 수 있습니다.<br>
먼저 스프링 프레임워크에서 제공하는 OncePerRequestFilter를 사용한 예제를 확인해보겠습니다.<br>

---
<br>

# 1. ApiCheckFilter 생성
---
<br>

![1](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/1.png)
<br>



# 2. 
---
<br>

![2](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/2.png)
<br>




# 3. 
---
<br>

![3](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/3.png)
<br>



# 4. 
---
<br>

![4](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/4.png)
<br>




# 5. 
---
<br>

![5](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/5.png)
<br>



# 6. 
---
<br>

![6](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/6.png)
<br>



# 7. 
---
<br>

![7](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/7.png)
<br>



# 8. 
---
<br>

![8](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/8.png)
<br>


