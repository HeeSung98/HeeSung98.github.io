---
layout: post
title: "[Spring] Thymeleaf의 inline 속성"
subtitle: Spring
date: '2023-03-16 08:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Thymeleaf`의 `inline 속성`에 대해 알아봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

Thymeleaf의 여러 속성 중 개발에 많은 도움을 주는 inline 속성에 대해 알아보겠습니다.<br>
inline 속성은 주로 javaScrpit 처리에서 유용하게 사용합니다.

---
<br>

# 1. SampleController 코드 추가
---
<br>

![1](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/1.PNG)
<br>

예제를 위해 SapleController에 코드를 추가로 작성합니다.<br>
작성한 exInline()은 RedirectAttributes를 사용해 /ex3로 result와 dto라는 이름의 데이터를 전달합니다. result는 단순한 문자열이고 dto는 SapleDTO의 객체입니다.<br>

# 2. ex3.html 생성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/2.PNG)
<br>

ex3.html을 통해 화면으로 확인할 수 있기 때문에 templates 폴더에 ex3.html 파일을 추가합니다.<br>


# 3. th:inline 코드 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/3.PNG)
<br>

ex3.html에서 \<script\> 태그 내에 사용된 th:inline 속성으로 인해 많은 변화가 생깁니다.<br>
브라우저에서 /sample/exInline으로 호출을 하면 ex3로 리다이렉트 되기 떄문에 결과 페이지는 아래와 같이 보여집니다.<br>


# 4. th:inline 결과 확인
---
<br>

![4](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/4.PNG)
<br>

위의 그림에서 오른쪽에 생성된 자바스크립트 부분을 살펴보겠습니다.<br>
별도의 처리가 없음에도 문자열은 자동으로 ""이 추가되어 문자열이 되고 dto 객체는 JSON 포맷의 문자열이 된 것을 확인할 수 있습니다.<br>

# 5. th:block 코드 작성
---
<br>

![5](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/5.PNG)
<br>

Thymeleaf의 th:block는 태그에 붙어서 th:text나 th:value 등을 써야하는 제약이 없기 떄문에 유용하게 사용할 수 있는 기능입니다.<br>
th:block를 통해 sno가 5의 배수일 경우 sno를, 아닌 경우에는 first를 출력하는 예제를 ex2.html에 기존 코드를 지우고 다시 작성해보겠습니다.

# 6. th:block 결과 확인
---
<br>

![6](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/6.PNG)
<br>

/sample/ex2의 실행 결과는 위의 그림과 같습니다.<br>
th:block은 실제 화면에서 html로 처리가 되지 않기 떄문에 위와 같이 루프 등을 별도로 처리할 때 많이 사용됩니다.<br>

# 7. Thymeleaf의 링크 처리
---
<br>

![7](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/miss.PNG)
<br>

Thymeleaf의 링크는 '@{}'를 이용해 처리합니다.<br>
실습을 위해 기존의 SampleController의 exModel()에  GetMapping의 value값을 '{}'로 처리해 다중 URL으로 지정합니다.<br>


# 8. th:href 코드 작성
---
<br>

![8](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/7.PNG)
<br>

exLink.html을 Templates폴더에 작성합니다.<br>
코드를 살펴보면 '@{}'로 구성된 링크를 처리하고 있는 것을 확인할 수 있습니다.<br>


# 9. th:href 결과 확인
---
<br>

![9](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/8.PNG)
<br>

그림의 결과를 보면 글들이 링크 처리 되어있는 것과 개발자 도구를 통해 /sample/exView로 넘어가게 될 것을 알 수 있습니다.<br>


# 10. 링크에 파라미터 추가
---
<br>

![10](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/9.PNG)
<br>

단순히 /sample/exView/로 하나만의 링크가 아닌 sno와 같은 파라미터를 추가해 링크를 키와 값의 형태로 만들 수 있습니다.<br>
코드를 살펴보면 exView 뒤에 ()를 추가하고 파라미터의 이름과 값을 적어주는 것을 알 수 있습니다.<br>

# 11. 링크에 파라미터 추가 결과
---
<br>

![11](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/10.PNG)
<br>

실행 결과 각 글들의 링크를 개발자 도구를 통해 살펴보면 exView 뒤에 ?sno=n이 추가된 것을 확인할 수 있습니다.<br>

# 12. 변수를 path로 사용
---
<br>

![12](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/11.PNG)
<br>

키와 값 형태 뿐만 아니라 단순히 변수를 path로 사용할 수 있습니다.<br>
코드를 살펴보면 dto.sno를 가져와 '{sno}'에 매핑시키는 것을 확인할 수 있습니다.

# 13. 변수를 path로 사용 결과
---
<br>

![13](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/12.PNG)
<br>

실행 결과 개발자 도구를 살펴보면 /sample/exView/n으로 단순히 sno가 path로 사용되는 것을 확인할 수 있습니다.<br>