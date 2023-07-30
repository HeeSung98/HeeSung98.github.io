---
layout: post
title: "[Spring] API를 위한 인증처리"
subtitle: Spring
date: '2023-05-22 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

특정한 URL로 외부에서 로그인이 가능하도록 해봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

API를 이용한다면 일반적인 로그인의 URL이 아닌 별도의 URL로 로그인을 처리하는 것이 일반적입니다. 폼 방식의 로그인과 달리 API는 URL이 변경되면 API를 이용하는 입장에서는 호출하는 URL을 변경해야만 하기 때문에 위험한 일입니다.<br>
API를 사용하기 위해 별도의 메뉴로 승인을 받는 것이 일반적이지만 일반 로그인과 동일한 계정으로 로그인하면 일정 기간동안 API를 호출할 수 있도록 구성합니다.<br>

---
<br>

# 1. ApiLoginFilter 생성
---
<br>

![1](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/1.png)
<br>

ApiLoginFilter를 위 그림과 같은 경로에 생성합니다.<br>
ApiLoginFilter는 AbstractAuthenticationProcessingFilter를 상속받아 작성합니다. AbstractAuthenticationProcessingFilter는 추상클래스로 설계되어 있고, attemptAuthentication()이라는 추상 메서드와 문자열로 패턴을 받는 생성자가 필요합니다. attemptAuthentication() 내부에는 파라미터로 email을 추출하고 해당 email이 null일 경우 에러를 출력하도록 작성합니다.<br>


# 2. SecurityConfig - filterChain() 수정
---
<br>

![2](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/2.png)
<br>

filterChain()에서 작성한 ApiLoginFilter를 추가합니다.<br>
apiCheckFilter 뒤에 apiLoginFilter가 동작하도록 addFilterbefor()를 사용합니다. apiLoginFilter의 경우 AuthenticationManager가 반드시 필요합니다. 따라서 파라미터에 AuthenticationManager를 작성합니다.<br>


# 3. SecurityConfig - apiLoginFilter() 생성
---
<br>

![3](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/3.png)
<br>

작성한 ApiLoginFilter를 빈으로 등록합니다.<br>
ApiLoginFilter는 '/api/login'이라는 경로로 접근할 때 동작하도록 지정합니다.<br>

# 4. ApiLoginFiter 생성 결과
---
<br>

![4](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/4.png)
<br>

프로젝트를 실행한 뒤 '/api/login' 경로로 이메일 파라미터 없이 접근할 경우 위 그림과 같이 401 에러가 발생하는 것을 확인할 수 있습니다.


# 5. ApiCheckFilter - checkAuthHeader() 생성
---
<br>

![5](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/5.png)
<br>

API를 호출하는 클라이언트에서는 다른 서버나 Application으로 실행되기 때문에 쿠키나 세션을 활용할 수 없습니다. 이러한 제약 때문에 API를 호출하는 경우에는 Request를 전송할 때 Http 헤더 메세지에 특별한 값을 지정해서 전송합니다.<br>
ApiCheckFilter에 checkAuthHeader()를 생성해 Request의 헤더 메세지를 확인하도록 작성합니다.<br>
ApiCheckFilter에서 Autorication 헤더를 파악해 checkAuthHeader()에 넘기고 checkAuthHeader()에서 헤더가 올바른지 확인한 후 T/F를 반환하도록 작성합니다.<br>


# 6. YARC - Authrization Header 추가 request 결과
---
<br>

![6](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/6.png)
<br>

YARC를 통해 헤더 검증 과정이 정상적으로 작동하는지 확인합니다.<br>
Custom Headers에 Authorization 헤더를 추가하고 헤더의 값으로 지정해둔 '12345678'을 작성한 뒤 'notes/1'에 접근합니다.<br>
request 결과 정상적으로 note의 내용을 가져오는 것을 확인할 수 있습니다.<br>


# 7. YARC - Authrization Header 제거 request 결과
---
<br>

![7](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/7.png)
<br>

만약 Authorization 헤더를 제거한 뒤 request할 경우 위와 같이 Respon Status는 OK라고 나오지만 note의 내용을 가져오지 못하는 것을 확인할 수 있습니다.<br>

# 8. ApiCheckFilter - doFilterInteral() 수정
---
<br>

![8](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/8.png)
<br>


Authorization 헤더 없이 request를 한 경우에도 Respon Status가 OK라고 나오는 이유는 ApiCheckFilter가 스프링 시큐리티가 사용하는 쿠키나 세션을 사용하지 않기 때문에 발생하는 문제입니다. 이를 해결하기 위해서는 AuthenticaitonManager를 이용하는 방식을 사용하는 방식과 JSON 포맷의 에러 메세지를 전송하는 방법을 사용할 수 있습니다. 이 중 후자의 방법으로 doFilterInternal()을 수정해 JSON 포맷의 에러 메세지를 전송하도록 작성합니다.<br>
앞서 checkHeader의 분기문에서 False일 경우 response의 상태를 FORBIDDEN으로 지정해주고 json객체를 만든 뒤 메세지와 에러 코드를 담아 response에 담는 형태로 작성합니다.<br>


# 9. ApiCheckFilter - doFilterInteral() 수정 결과
---
<br>

![9](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/9.png)
<br>

이제 Authorization 헤더 없이 request할 경우 에러가 발생하는 것을 확인할 수 있습니다.<br>


# 10. ApiLoginFilter - attemptAuthentication() 수정
---
<br>

![10](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/10.png)
<br>

ApiLoginFilter가 정상적으로 동작하기 위해서는 내부적으로 AuthenticationManager를 사용해 동작하도록 수정해야 합니다.<br>
AuthenticationManager는 authentication() 메소드를 보유하고 있습니다. 이 메소드의 파라미터와 리턴타입은 Authentication이라는 객체를 동일하게 사용합니다. 이 객체는 Token을 사용하는데 UsernamePasswordAuthenticationToken을 사용해 인증을 진행하도록 작성합니다.<br>
request에서 가져온 email과 pw를 사용해 UsernamePasswordAuthenticationToken을 발급하고 이를 반환하도록 attemptAuthentication()을 수정합니다.<br>


# 11. ApiLoginFilter - attemptAuthentication() 수정 결과
---
<br>

![11](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/11.png)
<br>

프로젝트를 실행한 후 'api/login?email=xxx&password=xxx'와 같이 데이터베이스에 존재하는 계정으로 API 로그인을 시도할 경우 정상적으로 로그인 되고 위와 같이 스택 트레이스에서 확인할 수 있습니다.<br>


# 12. ApiLoginFailHandler 생성
---
<br>

![12](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/12.png)
<br>

ApiLoginFilter로 인증처리를 수행하였고 이제 인증 후 성공/실패에 따른 처리를 진행해야 합니다. 이러한 처리를 위해 ApiLoginFailHandler를 위 그림과 같은 경로에 생성합니다.<br>
인증에 성공하는 경우 클라이언트가 보관할 인증 토큰이 전송되어야 하고 실패할 경우 JSON 결과를 전송하도록 해야합니다. AbstractAuthenticationProcessingFilter에는 setAuthenticationFailureHandler()를 이용해 인증에 실패했을 경우 처리를 지정할 수 있습니다.<br>
ApiLoginFailHandler는 AuthenticationFailureHandler를 상속받아 오직 인증에 실패할 경우의 처리를 전담하도록 구현합니다. 앞서 사용했던 방식과 같이 setStatus를 설정하고 json으로 메세지를 전송하도록 작성합니다.


# 13. SecurityConfig - ApiLoginFilter() 수정
---
<br>

![13](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/ee.png)
<br>

등록해둔 ApiLoginFilter() 빈에 setAuthenticationFailureHandler()를 사용해 작성한 ApiLoginFailHandler를 적용합니다.<br>


# 14. ApiLoginFailHandler 생성 결과
---
<br>

![13](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/13.png)
<br>

ApiLoginFailHandler를 적용한 후 잘못된 로그인을 시도할 경우 위와 같이 json포맷의 데이터가 출력된 것을 확인할 수 있습니다.<br>


# 15. ApiLoginFilter - successfulAuthentication() 작성
---
<br>

![14](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/14.png)
<br>

인증을 성공할 경우의 처리는 실패 처리와 마찬가지로 별도의 클래스를 작성할 수 있지만 상속받은 ApiLoginFilter에서 successfulAuthentication()를 재정의하는 방법으로도 구현할 수 있습니다.<br>


# 16. ApiLoginFilter - successfulAuthentication() 작성 결과
---
<br>

![15](/assets/img/web/spring/2023-05-22-[Spring]_API를_위한_인증처리/15.png)
<br>

successfulAuthentication()을 재정의한 후 정상적인 로그인을 시도할 경우 스택 트레이스에서 successfulAuthentication()에서 작성한 log가 출력되는 것을 확인할 수 있습니다.<br>
