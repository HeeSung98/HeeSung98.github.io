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

먼저 `@EnableGlobalMethodSecurity`를 작성합니다. @EnableGlobalMethodSecurity은 어노테이션 기반의 접근 제한을 설정할 수 있도록 하게하며 시큐리티 관련 설정 클래스에 작성합니다. 속성으로 securedEnabled와 prePostEnable을 작성했는데 이는 각각 예전의 `@Secure`를 사용 가능한지 지정하는 것과 `@PreAuthorize`를 사용 가능한지 지정하는 역할을 수행합니다.<br>
어노테이션 기반 접근 제한을 확인하기 위해 filterChain()에 작성된 requestMathers()를 동작하지 않게 합니다.<br>

# 2. SecurityConfig - filterChain() 수정 결과
---
<br>

![2](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/2.png)
<br>

그 결과 'sample/admin' 페이지에 아무 문제없이 접근할 수 있음을 확인할 수 있습니다.<br>


# 3. SampleController - exAdmin() 수정
---
<br>

![3](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/3.png)
<br>

컨트롤러의 exAdmin()에 `@PreAuthorize`를 작성합니다. @PreAuthorize의 속성으로 역할을 지정합니다.<br>


# 4. SampleController - exAdmin() 수정 결과
---
<br>

![4](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/4.png)
<br>

@PreAuthorize를 지정한 후 'sample/admin'에 접근한 결과 로그인을 요구하는 것을 확인할 수 있습니다.<br>


# 5. SampleController - exMember(), exAll() 수정
---
<br>

![5](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/5.png)
<br>

exMember() 역시 member의 역할을 가진 유저만 접근할 수 있도록 수정합니다.<br>
exAll()은 모든 유저가 접근할 수 있도록 @PreAuthorize의 파라미터로 "permitAll()"을 작성합니다.<br>


# 6. SampleController - exMemberOnly() 작성
---
<br>

![6](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/6.png)
<br>

@PreAuthorize는 유저의 권한을 통해 접근을 제어하는 것이 아닌 특별히 지정한 유저만 접근할 수 있도록 하는 기능 또한 가지고 있습니다.<br>
@PreAuthorize의 value 표현식은 '#'과 같은 특별한 기오나 authentication과 같은 내장 변수를 이용할 수 있습니다.<br>
clubAuthMemberDTO의 username이 지정한 이메일 계정과 같을 경우에만 접근할 수 있도록 설정한 뒤 결과를 살펴보겠습니다.<br>


# 7. SampleController - exMemberOnly() 결과 1
---
<br>

![7](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/7.png)
<br>

권한을 부여받은 아이디로 'sample/exOnly'에 접근할 경우 정상적으로 이동할 수 있는 것을 확인할 수 있습니다.<br>


# 8. SampleController - exMemberOnly() 결과 2
---
<br>

![8](/assets/img/web/spring/2023-05-15-[Spring]_PreAuthorize를_사용한_접근_제한/8.png)
<br>

권한을 부여받지 못한 사용자는 Acess Denied 에러 화면을 보는 것을 확인할 수 있습니다.<br>
