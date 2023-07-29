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

OncePerRequestFilter는 추상 클래스로 제공되는 필터로 가장 일반적이며, 매번 동작하는 기본적인 필터입니다. ApiCheckFilter를 위의 그림과 같은 경로에 생성한 뒤 OncePerRequestFilter를 상속받도록 작성합니다.<br>
우선은 단순히 log를 출력하도록 작성하고 filterChain.doFilter()를 통해 다음 단계로 넘어가게 합니다.<br>

# 2. SecurityConfig - apiCheckFilter() 작성
---
<br>

![2](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/2.png)
<br>

생성한 ApiCheckFilter를 SecurityConfig에서 스프링의 빈으로 등록합니다.<br>


# 3. SecurityConfig - apiCheckFilter() 작성 결과
---
<br>

![3](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/3.png)
<br>

프로젝트를 실행해 중간의 스택 트레이스를 살펴보면 ApiCheckFilter가 동작하는 것을 확인할 수 있습니다.<br>
ApiCheckFilter의 경우 스택 트레이스에서 보여지는 (15/15)를 통해 여러 과정 중 가장 마지막 필터임을 알 수 있습니다.<br>

# 4. SecurityConfig - finterChain() 수정
---
<br>

![4](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/4.png)
<br>

만약 ApiCheckFilter의 동작 순서를 조절하고 싶은 경우 http.addFilterBefore()을 사용할 수 있습니다.<br>
위와 같이 addFilterBefore()를 작성할 경우 AuthenticationFilter 이전에 ApiCheckFilter가 작동하도록 순서가 변경됩니다.<br>


# 5. SecurityConfig - finterChain() 수정 결과
---
<br>

![5](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/5.png)
<br>

필터 동작 순서를 변경한 뒤 프로젝트를 실행하고 스택 트레이스를 살펴보면 ApiCheckFilter의 동작 순서가 바뀐 것을 확인할 수 있습니다.<br>


# 6. ApiCheckFilter 수정
---
<br>

![6](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/6.png)
<br>

ApiCheckFilter가 오직 '/notes'로 시작하는 경우에만 작동하도록 하고자 합니다. 이는 AntPathMatcher를 사용해 구현할 수 있습니다. AntPathMatcher는 엔트 패턴에 맞는지를 검사하는 유틸리티입니다.<br>
생성자에 AntPathMathcer()를 추가하고 doFilterInternal()에 AntPathMatcher의 match()를 사용해 지정한 패턴과 request의 URI가 같을 때 실행되도록 작성합니다.<br>


# 7. SecurityConfig - apiCheckFilter() 수정
---
<br>

![7](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/7.png)
<br>

생성자에 파라미터가 생겼기 때문에 apiCheckFilter()를 수정합니다.<br>

# 8. ApiCheckFilter 수정 결과
---
<br>

![8](/assets/img/web/spring/2023-05-18-[Spring]_API_서비스_필터링/8.png)
<br>

수정 후 프로젝트를 실행하면 '/notes/'로 접근할 경우에만 스택 트레이스에 ApiCheckFilter가 동작하는 것을 확인할 수 있습니다.<br>
