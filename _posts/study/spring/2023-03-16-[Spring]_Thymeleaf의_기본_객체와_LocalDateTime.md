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

`Thymeleaf`의 기본 객체와 LocalDateTime에 대해 알아봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

---
<br>

# 1. SampleDTO 클래스 생성 및 작성
---
<br>

![1](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/1.PNG)
<br>

실습을 위해 그림의 표시해둔 경로로 SampleDTO 클래스를 생성합니다.<br>
`@Data` 어노테이션은 Getter/Setter, toString(), equeals(), hashCode()를 자동으로 생성해주는 어노테이션입니다.<br>

# 2. SampleController 클래스 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/2.PNG)
<br>

SampleController에서, 작성된 SampleDTO의 객체를 Mdoel에 추가해 전달합니다.<br>
exModel()은 나중에 다양하게 Thymeleaf를 실습하기 위해 URL 변경이 용이하게 작성합니다.<br> @GetMapping의 value 속성값을 '{}'로 처리하면 하나 이상의 URL을 지정할 수 있습니다.<br>
SampleDTO 타입의 객체 20개를 추가한 뒤 Model에 담아 전송합니다.<br>

# 3. 반복문 처리
---
<br>

![3](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/3.PNG)
<br>

Thymeleaf에서 반복은 th:each라는 속성을 사용합니다.<br>
templates 폴더 내에 있는 sample 폴더에 ex2.html 파일을 생성합니다.<br>
\<li\> 태그 내에 dto라는 변수를 만들어서 사용하고 Model로 전달된 데이터는 ${list}를 이용해 처리합니다.


# 4. 반복문 처리 실행 결과
---
<br>

![4](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/4.PNG)
<br>

/sample/ex2의 실행 결과는 위의 그림과 같습니다.<br>

# 5. 반복문의 상태 객체
---
<br>

![5](/assets/img/study_Web/spring/2023-03-16-[Spring]_Thymeleaf의_기본_객체와_LocalDateTime/5.PNG)
<br>

반복문에는 부가적으로 상태(state) 객체가 존재합니다. 상태 객체를 이용하면 순번이나 인덱스 번호 또는 홀수/짝수 여부를 나타낼 수 있습니다.<br>
그림의 코드를 살펴보면 state 변수가 추가된 것을 확인할 수 있습니다. state 객체는 index와 count의 속성을 사용할 수 있습니다.