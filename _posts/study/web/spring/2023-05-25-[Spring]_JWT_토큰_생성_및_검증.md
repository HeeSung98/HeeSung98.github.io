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

`JWT`란 JSON Web Token의 약자로 선택적 서명 및 선택적 암호화를 사용하여 데이터를 만들기 위한 인터넷 표준입니다.<br>
JWT를 사용해 인증에 성공한 후 사용자가 API를 호출할 때 JWT를 사용해 전송하게 합니다. API를 호출할 때는 JWT가 포함된 문자열을 읽어 해당 Request가 정상적인 요청인지를 확인합니다.<br>


---
<br>

# 1. JWT.io 사이트를 이용한 검증
---
<br>

![1](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/1.png)
<br>

JWT와 관련한 정보는 위 그림과 같은 'https://jwt.io' 사이트에서 알아볼 수 있습니다.<br>
위 화면에서 왼쪽은 실제로 주고받는 JWT 문자열이고 오른쪽은 이를 해석한 실제 구성 요소들입니다.<br>
오른쪽 하단에는 암호화를 할 때 사용하는 비밀 키를 입력할 수 있습니다. 이 비밀 키를 입력할 경우 왼쪽의 내용이 변경되는 것을 확인할 수 있습니다.<br>


# 2. build.gradle - jjwt 라이브러리 추가
---
<br>

![2](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/2.png)
<br>

JWT를 이용하기 위해서는 직접 코드를 구현하거나, Spring Security OAuth에서 제공하는 클래스가 있지만 사용하기 쉬운 라이브러리인 'io.jsonwebtoken'을 이용해 개발합니다.<br>


# 3. JWTUtil 생성
---
<br>

![3](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/3.png)
<br>

JWT는 인증에 성공했을 때 JWT 문자열을 만들어서 클라이언트에게 전송하는 것과, 클라이언트가 보낸 토큰의 값을 검증하는 경우 사용됩니다.<br>
위 그림과 같은 경로에 JWTUtil을 생성합니다. JWTUtil은 스프링 환경이 아닌 곳에서 사용할 수 있도록 간단한 유틸리티 클래스로 설계합니다.<br>
먼저 generateToken()을 작성합니다. JWT는 문자열 자체를 알 경우 누구나 API를 사용할 수 있다는 문제점이 있습니다. 따라서 setExpiration()을 통해 30일 뒤 만료되도록 설정하고 지정한 Signiture를 secretKey에 담아 signWith()에 매개변수로 사용합니다. 또한 sub라는 이름을 가지는 Claim에는 generateToken()에서 매개변수로 받아온 content를 담도록 작성합니다. content는 사용자의 이메일 주소를 입력해 나중에 사용할 수 있도록 구성합니다.<br>

# 4. JWTUtil - validateAndExtract() 작성
---
<br>

![4](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/4.png)
<br>

다음으로 validateAndExtract()를 작성합니다. validateAndExtract()는 JWT 문자열을 검증하는 메소드입니다.<br>
넘겨받은 tokenStr을 변환한 뒤 내용만 추출하도록 작성합니다. 또한 중간중간 로그를 남겨 해당 데이터들이 어떤 형태인지 확인할 수 있도록 합니다.<br>


# 5. JWTTests 생성
---
<br>

![5](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/5.png)
<br>

작성한 JWTUtil이 정상적으로 동작하는가를 확인하기 위한 JWTTests를 생성합니다.<br>
JWT에 관한 Test는 스프링을 이용하는게 테스트가 아니기 때문에 JWTUtil 객체를 직접 만들어 확인해보고 jwtUtil의 generateToken()의 매개변수로 지정한 이메일을 넣어 JWT를 생성하도록 작성합니다.<br>
이때 testBefore()의 경우 `@BeforeEach`를 사용하였는데 이 어노테이션은 별도로 실행하지 않아도 테스트 메소드를 실행할 경우 테스트 메소드 이전에 자동으로 실행됩니다. `@BeforeEach`뿐만 아니라 `@BeforeAll`, `@AfterAll` 등 다양한 어노테이션이 존재합니다.<br>

# 6. JWTTests - testEncode() 결과
---
<br>

![6](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/6.png)
<br>

testEncode()의 실행 결과는 위와 같습니다. testEncode()를 실행하기 전 testBefore()가 실행되는 것을 확인할 수 있고 그 뒤 JWT가 출력된 것을 볼 수 있습니다.<br>
이 JWT가 올바른가에 대한 검증은 앞서 1번에서 살펴본 사이트에서 수행할 수 있습니다.<br>

# 7. testEncode() 결과 검증
---
<br>

![7](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/7.png)
<br>

JWT를 검증할 때 비밀 키를 나중에 변경할 경우 왼쪽의 JWT 문자열 자체가 변경되기 때문에 먼저 오른쪽 하단에 Signiture를 입력합니다.<br>
그 후 testEncode()에서 얻은 문자열을 왼쪽에 입력할 경우 위의 그림과 같이 PAYLOAD에 테스트에서 사용한 email이 출력되는 것을 확인할 수 있습니다.<br>
또한 PAYLOAD의 exp부분에 마우스를 갖다댈 경우 만료되는 기간 역시 확인할 수 있습니다.<br>

# 8. JWTTests - testEncode() 수정
---
<br>

![8](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/8.png)
<br>

작성한 testEncode()에 validateAndExtract()를 추가합니다.<br>
또한 validateAndExtract()의 만료가 정상적으로 동작하는지 확인을 위한 Sleep(5000) 또한 추가합니다.<br>


# 9. JWTTests - testEncode() 수정 결과
---
<br>

![9](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/9.png)
<br>

생성한 JWT가 다시 resultEmail로 제대로 decode되는지 확인한 결과 정상적으로 'user95@test.com'이 출력되는 것을 확인할 수 있습니다.<br>

# 10. JWTUtil - generateToken() 수정
---
<br>

![10](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/10.png)
<br>

JWT에 대한 만료를 확인하기 위해 generateToken()의 만료 기간을 1초로 설정합니다.<br>


# 11. JWTUtil - generateToken() 수정 결과
---
<br>

![11](/assets/img/web/spring/2023-05-25-[Spring]_JWT_토큰_생성_및_검증/11.png)
<br>

만료 기간을 수정한 뒤 다시 testEncode()를 수행한 결과 정상적으로 ExpiredJwtException이 발생하는 것을 확인할 수 있습니다.<br>
