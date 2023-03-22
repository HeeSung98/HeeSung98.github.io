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

`Thymeleaf`의 inline 속성에 대해 알아봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

---
<br>

# 1. SampleDTO 클래스 생성 및 작성
---
<br>

![1](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/1.PNG)
<br>

실습을 위해 그림의 표시해둔 경로로 SampleDTO 클래스를 생성합니다.<br>
`@Data` 어노테이션은 Getter/Setter, toString(), equeals(), hashCode()를 자동으로 생성해주는 어노테이션입니다.<br>

# 2. SampleController 클래스 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/2.PNG)
<br>

SampleController에서, 작성된 SampleDTO의 객체를 Mdoel에 추가해 전달합니다.<br>
exModel()은 나중에 다양하게 Thymeleaf를 실습하기 위해 URL 변경이 용이하게 작성합니다.<br> @GetMapping의 value 속성값을 '{}'로 처리하면 하나 이상의 URL을 지정할 수 있습니다.<br>
SampleDTO 타입의 객체 20개를 추가한 뒤 Model에 담아 전송합니다.<br>

# 3. 반복문 처리
---
<br>

![3](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/3.PNG)
<br>

Thymeleaf에서 반복은 th:each라는 속성을 사용합니다.<br>
templates 폴더 내에 있는 sample 폴더에 ex2.html 파일을 생성합니다.<br>
\<li\> 태그 내에 dto라는 변수를 만들어서 사용하고 Model로 전달된 데이터는 ${list}를 이용해 처리합니다.


# 4. 반복문 처리 실행 결과
---
<br>

![4](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/4.PNG)
<br>

/sample/ex2의 실행 결과는 위의 그림과 같습니다.<br>

# 5. 반복문의 상태 객체
---
<br>

![5](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/5.PNG)
<br>

반복문에는 부가적으로 상태(state) 객체가 존재합니다. 상태 객체를 이용하면 순번이나 인덱스 번호 또는 홀수/짝수 여부를 나타낼 수 있습니다.<br>
그림의 코드를 살펴보면 state 변수가 추가된 것을 확인할 수 있습니다. state 객체는 index와 count의 속성을 사용할 수 있습니다.

# 6. 반복문의 상태 객체 실행 결과
---
<br>

![6](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/6.PNG)
<br>

/sample/ex2의 실행 결과는 위의 그림과 같습니다.<br>
4번에서 본 결과와 달리 0부터 시작하는 번호가 추가된 것을 알 수 있습니다.<br>

# 7. 제어문 처리 - th:if
---
<br>

![7](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/7.PNG)
<br>

Thymeleaf의 제어문 처리는 th:if~ unless와 삼항연산자 스타일이 존재합니다.<br>
우선 th:if를 통해 sno가 5의 배수인 list를 출력하는 코드는 위의 그림과 같습니다.<br>

# 8. 제어문 처리 - th:if 결과
---
<br>

![8](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/8.PNG)
<br>

실행 결과 sno가 5의 배수인 list만 출력되는 것을 확인할 수 있습니다.<br>

# 9. 제어문 처리 - th:unless
---
<br>

![9](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/9.PNG)
<br>

th:if와 th:unless를 사용하면 다른 내용을 출력하는 것이 가능합니다.<br>
Thymeleaf는 if~else가 하나의 묶음이 아닌 단독으로 처리합니다.<br>
sno가 5의 배수일 경우 sno만 출력하고 그렇지 않다면 first만 출력하는 코드는 위의 그림과 같습니다<br>

# 10. 제어문 처리 - th:unless 결과
---
<br>

![10](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/10.PNG)
<br>

실행 결과 sno가 5의 배수인 경우 first branch가, 아닌 경우 second branch가 출력되는 것을 확인할 수 있습니다.

# 11. 제어문 처리 - 삼항연산자
---
<br>

![11](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/11.PNG)
<br>

Thymeleaf의 삼항연산자를 사용하는 방식은 위의 그림과 같습니다.

# 12. 제어문 처리 - 삼항연산자 결과
---
<br>

![12](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_inline_속성/12.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>