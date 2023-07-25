---
layout: post
title: "[Spring] @PreAuthorize를 사용한 접근 제한"
subtitle: Spring
date: '2023-05-15 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

어노테이션 설정으로 지정된 URL에 접근 제한을 지정해봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

SecurityConfig를 사용해 접근 제한을 거는 방식은 매번 URL을 추가할 때마다 설정해야 하기 때문에 번거로운 작업입니다. 스프링 시큐리티는 이런 설정을 어노테이션만으로 지정할 수 있습니다.<br>

---
<br>

# 1. SecurityConfig - filterChain() 수정
---
<br>

![1](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/1.png)
<br>



# 2. SecurityConfig - filterChain() 수정 결과
---
<br>

![2](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/2.png)
<br>




# 3. SampleController - exAdmin() 수정
---
<br>

![3](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/3.png)
<br>



# 4. SampleController - exAdmin() 수정 결과
---
<br>

![4](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/4.png)
<br>




# 5. SampleController - exMember() 수정
---
<br>

![5](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/5.png)
<br>



# 6. SampleController - exMemberOnly() 작성
---
<br>

![6](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/6.png)
<br>



# 7. SampleController - exMemberOnly() 결과 1
---
<br>

![7](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/7.png)
<br>



# 8. SampleController - exMemberOnly() 결과 2
---
<br>

![8](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/8.png)
<br>


