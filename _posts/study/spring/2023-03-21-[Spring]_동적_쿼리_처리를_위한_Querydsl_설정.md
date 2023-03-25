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

앞서 공부한 내용을 하나로 조합해봅시다.

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

![1](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/1.PNG)
<br>

실습을 위해 SampleController에 위의 그림과 같은 exLayout1()을 추가합니다.<br>

# 2. fragment1.html 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/2.PNG)
<br>

이번에 구현하고자 하는 exLayout.html은 내부적으로 다른 파일에 있는 일부분을 조각처럼 가져와 구성합니다. 이러한 조각이 될 수 있는 fragments 폴더를 작성하고 조각이 될 fragment1.html을 생성한 뒤 위와 같은 내용을 작성합니다.<br>
th:fragment라는 태그를 통해 표현합니다.<br>

# 3. exLayout1.html 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/3.PNG)
<br>

이제 화면이 될 exLayout1.html을 추가한 뒤 fragment1.html의 조각들을 가져와 사용하는 코드를 작성합니다.<br>
th:replace, th:insert, th:bolck th:replace를 사용해 fragment1의 조각을 각각 다르게 가져와보겠습니다.<br>


# 4. exLayout1.html 실행 결과
---
<br>

![4](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/4.PNG)
<br>

실행 결과 개발자 도구를 살펴보면 가져온 결과가 다른 것을 확인할 수 있습니다.<br>
th:insert의 경우 th:replace와 달리 \<div\> 태그 내에 다시 \<div\> 태그가 생성된 것을 확인할 수 있습니다.<br>

# 5. fragment2.html 작성
---
<br>

![5](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/5.PNG)
<br>

이번엔 파일의 일부분을 가져오는 것이 아닌 파일의 전체를 가져오는 실습을 해보겠습니다.<br>
실습을 위해 fragment2.html을 생성한 뒤 위와 같은 코드를 작성합니다.<br>

# 6. exLayout1.html 코드 추가
---
<br>

![6](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/6.PNG)
<br>

exLayout1.html에는 작성된 fragment2.html의 전체를 가져오는 부분을 추가합니다.<br>
th:replace="~{/fragments/fragment2}"를 통해 fragment2의 전체를 가져옵니다.<br>

# 7. exLayout1.html 실행 결과
---
<br>

![7](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/7.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>

# 8. SampleController 코드 추가 (파라미터 방식)
---
<br>

![8](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/8.PNG)
<br>

이번엔 파라미터 방식의 처리를 실습해보기위해 SampleController에 /exLayout2를 추가하겠습니다.<br>

# 9. fragment3.html 작성
---
<br>

![9](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/miss.PNG)
<br>

fragment3.html에는 파라미터를 받는 th:fragment를 위의 그림과 같이 사용합니다.<br>
선언된 target에는 first와 second라는 파라미터를 받을 수 있도록 구성하였고 내부적으로 th:block에 표현되고 있습니다.<br> 

# 10. exLayout2.html 작성
---
<br>

![10](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/9.PNG)
<br>

실제 화면이 될 exLayout2.html을 작성합니다.<br>
ex2Layout2.html은 화면 구성과 관련된 기능이 없이 target에 파라미터만을 사용하는 것을 볼 수 있습니다. ulFirst, ulSecond가 fragment3의 내용의 일부로 전달되고 이를 사용하게 됩니다.

# 11. exLayout2.html 실행 결과
---
<br>

![11](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/10.PNG)
<br>

실행 결과 fragment3.html의 코드에 exLayout2.html에서 전달된 태그들이 포함되어 출력된 것을 확인할 수 있습니다.<br>

# 12. 레이아웃 템플릿 만들기
---
<br>

![12](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/11.PNG)
<br>

레이아웃 전체를 하나의 페이지로 구성하고 필요한 부분을 파라미터로 전달하는 방식으로 공통의 레이아웃을 사용할 수 있습니다.<br>
temlpates 폴더 내에 layout이라는 폴더를 생성하고 layout1.html을 작성합니다.

# 13. layout1.html 웹 브라우저로 실행
---
<br>

![13](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/12.PNG)
<br>

브라우저로 실행한 결과는 위의 그림과 같습니다.<br>

# 14. CONTENT 영역을 변경할 수 있도록 수정
---
<br>

![14](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/13.PNG)
<br>

실제 개발을 한다면 중간 CONTENT 영역이 다른 내용으로 변경할 수 있도록 만들어야 합니다.<br>
화면 전체를 하나의 템플릿으로 만들고 중간의 CONTENT 영역을 변경 가능하도록 수정합니다.<br>
상단에 th:fragment를 setContent로 지정해 content라는 파라미터를 받을 수 있게 합니다.<br>
화면 중간은 파라미터로 전달되는 content를 표시하게 합니다.<br>
하단부에는 작성한 th:block을 닫아주는 코드를 작성합니다.<br>

# 15. exTemplate.html 작성
---
<br>

![15](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/14.PNG)
<br>

exTemplate.html을 위와 같이 작성합니다.<br>
이 때 SampleController에 /exTemplate를 작성 완료한 상태입니다.<br>
파일 전체 내용은 layout1.html로 전달하고 현재 파일에 적은 content 부분을 전달합니다.

# 16. exTemplate.html 실행 결과
---
<br>

![16](/assets/img/study_Web/spring/2023-03-21-[Spring]_프로젝트_구조_만들기/15.PNG)
<br>

실행 결과는 위의 그림과 같습니다.<br>
exTemplate.html에서 작성한 exTemplate Page를 content에 담아 layout1에 넘겨주었고 전체적인 레이아웃으로 layout1.html의 내용이 사용된 것을 확인할 수 있습니다.