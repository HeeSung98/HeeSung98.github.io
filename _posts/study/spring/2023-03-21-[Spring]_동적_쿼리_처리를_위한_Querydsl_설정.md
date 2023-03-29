---
layout: post
title: "[Spring] 동적 쿼리 처리를 위한 Querydsl 설정"
subtitle: Spring
date: '2023-03-21 10:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Querydsl`을 사용하기 위한 설정을 해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
Thymeleaf의 레이아웃은 JSP의 include와 같이 특정 부분을 외부, 내부에서 가져와 포함하는 형태와 특정한 부분을 파라미터로 전달해 내용에 포함하는 형태로 두 가지의 방식이 존재합니다. 먼저 include 형태부터 살펴보겠습니다.

---
<br>

# 1. SampleController 코드 추가 (include 방식)
---
<br>

![1](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/1.PNG)
<br>

실습을 위해 SampleController에 위의 그림과 같은 exLayout1()을 추가합니다.<br>

# 2. fragment1.html 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/2.PNG)
<br>

이번에 구현하고자 하는 exLayout.html은 내부적으로 다른 파일에 있는 일부분을 조각처럼 가져와 구성합니다. 이러한 조각이 될 수 있는 fragments 폴더를 작성하고 조각이 될 fragment1.html을 생성한 뒤 위와 같은 내용을 작성합니다.<br>
th:fragment라는 태그를 통해 표현합니다.<br>

# 3. exLayout1.html 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/3.PNG)
<br>

이제 화면이 될 exLayout1.html을 추가한 뒤 fragment1.html의 조각들을 가져와 사용하는 코드를 작성합니다.<br>
th:replace, th:insert, th:bolck th:replace를 사용해 fragment1의 조각을 각각 다르게 가져와보겠습니다.<br>


# 4. exLayout1.html 실행 결과
---
<br>

![4](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/4.PNG)
<br>

실행 결과 개발자 도구를 살펴보면 가져온 결과가 다른 것을 확인할 수 있습니다.<br>
th:insert의 경우 th:replace와 달리 \<div\> 태그 내에 다시 \<div\> 태그가 생성된 것을 확인할 수 있습니다.<br>

# 5. fragment2.html 작성
---
<br>

![5](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/5.PNG)
<br>

이번엔 파일의 일부분을 가져오는 것이 아닌 파일의 전체를 가져오는 실습을 해보겠습니다.<br>
실습을 위해 fragment2.html을 생성한 뒤 위와 같은 코드를 작성합니다.<br>

# 6. exLayout1.html 코드 추가
---
<br>

![6](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/6.PNG)
<br>

exLayout1.html에는 작성된 fragment2.html의 전체를 가져오는 부분을 추가합니다.<br>
th:replace="~{/fragments/fragment2}"를 통해 fragment2의 전체를 가져옵니다.<br>

# 7. exLayout1.html 실행 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-03-21-[Spring]_동적_쿼리_처리를_위한_Querydsl_설정/7.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>
