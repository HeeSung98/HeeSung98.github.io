---
layout: post
title: "[Spring] Thymeleaf의 기본 객체와 LocalDateTime"
subtitle: Spring
date: '2023-03-16 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Thymeleaf`의 `기본 객체와 LocalDateTime`에 대해 알아봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
Thymeleaf는 여러 종류의 개본 객체를 지원합니다.<br>
기본 객체는 문자, 숫자, 팔미터, request 등 다양하게 존재하는데 이를 사용해 JSP와 유사하거나 좀 더 편리하게 코드를 작성할 수 있습니다.

---
<br>

# 1. #numbers를 사용한 숫자 포매팅
---
<br>

![1](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/1.PNG)
<br>

Thymeleaf의 #numbers를 사용하면 별도의 설정 없이 편리하게 숫자를 포매팅할 수 있습니다.<br>
위의 코드를 살펴보면 dto.sno를 다섯 자리로 만드는 코드인 것을 유추할 수 있습니다.<br>

# 2. 숫자 포매팅 결과
---
<br>

![2](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/2.PNG)
<br>

포매팅 결과 sno가 다섯 자리로 출력되고 있는 것을 확인할 수 있습니다.<br>

# 3. LocalDate타입의 편리한 처리를 위한 의존성 주입
---
<br>

![3](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/3.PNG)
<br>

아쉽게도 Thymeleaf는 LocalDateTime에 대해서 상당히 복잡한 처리를 해야하는 단점이 있습니다. 하지만 thymeleaf-extras-java8time을 이용하면 이를 좀 더 편리하게 처리할 수 있습니다.<br>
thymeleaf-extras-java8time를 사용하기 위한 의존성 주입은 위의 그림과 같습니다.<br>


# 4. #temporlas를 사용한 LocalDateTime 포매팅
---
<br>

![4](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/4.PNG)
<br>

LocalDateTime을 포매팅 하는 코드는 위의 그림과 같습니다.<br>

# 5. LocalDateTime 포매팅 결과
---
<br>

![5](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/5.PNG)
<br>

위의 그림과 같이 LocalDateTime이 간단히 포매팅 된 것을 확인할 수 있습니다.<br>