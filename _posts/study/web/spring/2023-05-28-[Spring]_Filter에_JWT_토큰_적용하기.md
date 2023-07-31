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

ApiLoginFilter/ApliCheckFilter에 JWT를 적용해봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

JWT에 대한 생성과 검증을 수행했으니 이제 이를 필터에 적용하고자 합니다.
이를 위해 각 필터의 생성자에 jwtUtil을 주입하고 적용할 수 있도록 필터를 수정합니다.<br>

---
<br>

# 1. SecurityConfig - jwtiUtil() 생성
---
<br>

![1](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/1.png)
<br>

SecurityConfig에 jwtUtil()을 빈으로 등록합니다.<br>

# 2. ApiLoginFilter - jwtUtil 추가
---
<br>

![2](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/2.png)
<br>

먼저 ApiLoginFiilter의 생성자를 통해 JWTUtil을 주입받는 구조로 수정합니다.


# 3. ApiLoginFilter - successfulAuthentication() 수정
---
<br>

![3](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/3.png)
<br>

주입받은 JWTUtil을 이용해 successfulAuthentication() 내에서 문자열을 발행해 줍니다. 그 후 respon.getOutputStream()을 통해 토큰을 화면에 출력하도록 코드를 수정합니다.<br>

# 4. ApiLoginFilter - jwtUtil 추가 결과
---
<br>

![4](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/4.png)
<br>

프로젝트를 실행한 뒤 'api/login'에 email과 pw를 정상적으로 입력한 뒤 접근할 경우 브라우저에 JWT 문자열이 출력된 것을 확인할 수 있습니다.<br>


# 5. ApiCheckFilter - jwtUtil 추가
---
<br>

![5](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/5m.png)
<br>

ApiCheckFilter의 경우 Authorization 헤더 메세지를 통해 JWT를 확인하도록 수정해야 합니다.<br>
ApiCheckFilter도 마찬가지로 생성자를 통해 JWTUtil을 주입받도록 수정합니다.<br>

# 6. ApiCheckFilter - checkAuthHeader() 수정
---
<br>

![6](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/6m.png)
<br>

checkAuthHeader()의 내부에 validateAndExtract()를 호출하도록 코드를 작성합니다.<br>
Authorization 헤더 메세지의 경우 인증 타입을 이용하는데 일반적으로 'Basic'을 사용하고, JWT를 이용할 때는 'Bearer'를 사용합니다. request의 헤더 메세지가 Authorization이고 Bearer로 시작할 경우 validateAndExtract()를 통해 디코드 하는 형태로 작성합니다.<br>

# 7. SecuriyConfig - apiCheckFilter(), apiLoginFilter() 수정
---
<br>

![7](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/e.png)
<br>

두 필터의 생성자를 변경했기 때문에 SecuriyConfig에서도 그에 맞게 JWTUtil을 주입하도록 수정합니다.<br>

# 8. YARC - JWT Header 추가 request
---
<br>

![8](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/8.png)
<br>

이제 YARC에서 JWT를 이용한 검증이 제대로 이루어지는가를 확인합니다.<br>
'/notes/1'에 대한 GET request를 Authorizaion 헤더를 추가해 수행합니다. Authorizaion 헤더는 'Bearer'와 공백으로 시작한 뒤 JWT 문자열을 추가합니다.<br>


# 9. YARC - JWT Header 추가 request 결과
---
<br>

![9](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/9.png)
<br>

request 결과 정상적으로 1번 notes를 확인할 수 있습니다.

# 10. YARC - JWT Header 제거 request 결과
---
<br>

![10](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/10.png)
<br>

 Authorizaion 헤더를 제거하고 request할 경우 작성해둔 FAIL CHECK API TOKEN 에러가 출력되는 것을 확인할 수 있습니다.<br>

# 11. CORSFilter 생성
---
<br>

![11](/assets/img/web/spring/2023-05-28-[Spring]_Filter에_JWT_토큰_적용하기/11.png)
<br>


