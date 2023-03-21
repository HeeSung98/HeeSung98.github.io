---
layout: post
title: "[Spring] Thymeleaf를 사용하는 프로젝트 생성"
subtitle: Spring
date: '2023-03-14 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Thymeleaf`를 사용하는 프로젝트를 생성해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

`Thymeleaf`는 전체적인 화면을 디자인할 때 사용되는 뷰 템플릿입니다.<br>
Thymeleaf를 사용하는 이유는 JSP와 유사하게 ${}를 별도의 처리 없이 이용할 수 있고, Model에 담긴 객체를 화면에서 JavaScrpit로 처리하기 편하며, .html 파일로 생성하는데 문제없을뿐더러, 별도의 확장자를 이용하지 않기 때문입니다.<br>
이러한 Thymeleaf를 사용하는 프로젝트를 생성해보겠습니다.<br>

---
<br>

# 1. Thymeleaf를 사용하는 프로젝트 생성
---
<br>

![1](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/1.PNG)
<br>

프로젝트의 생성은 위의 그림과 같이 진행합니다.<br>
프로젝트의 이름과 Artifact는 자유롭게 작성합니다.<br>

# 2. 프로젝트 의존성 설정
---
<br>

![2](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/2.PNG)
<br>

생성할 프로젝트의 의존성은 그림과 같이 사용합니다.<br>
Sprint Boot DevTools, Lombok, Spring Web, Thymeleaf로 네 가지의 의존성을 추가합니다.<br>

# 3. application.properties 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/3.PNG)
<br>

Thymeleaf의 경우 변경 후에 만들어진 결과를 보관하지 않도록 설정하는 것이 편리합니다. 따라서 프로젝트 생성 시 만들어진 application.properties에 그림과 같은 내용을 작성합니다.<br>


# 4. SampleController 생성 및 작성
---
<br>

![4](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/4.PNG)
<br>

생성된 프로젝트 내에 controller 패키지를 생성하고 SampleController를 추가합니다.<br>
SampleController의 동작을 확인하기 위해 `@Log4j2`를 사용했습니다. @Log4j2는 콘솔 및 파일 출력의 형태로 로깅을 도와주는 어노테이션입니다.<br>

# 5. ex1.html 생성
---
<br>

![5](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/5.PNG)
<br>

Thymeleaf는 프로젝트 생성 시 추가되는 templates 폴더를 기본으로 사용합니다.<br> temlplates 폴더 내에 sample 폴더를 생성 후 ex1.html 파일을 추가합니다.<br>

# 6. ex1.html 생성
---
<br>

![6](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/6.PNG)
<br>

ex1.html의 코드는 그림과 같이 작성합니다.<br>
<html> 태그 내에 xmlns 속성을 작성한 뒤 thymeleaf 속성값을 지정합니다. Intellij Ultimate는 Thymeleaf 관련 플러그인이 기본으로 설치되어있지만 xmlns 속성을 지정해 좀 더 좋은 코드 완성을 도와주게 합니다.

# 7. ex3.Apllication 실행
---
<br>

![7](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/7.PNG)
<br>

ex3Application을 실행시킵니다.<br>

# 8. /sample/ex1 실행 결과 확인
---
<br>

![8](/assets/img/study_Web/spring/2023-03-14-[Spring]_Thymeleaf를_사용하는_프로젝트_생성/8.PNG)
<br>

웹 브라우저에 들어가 /sample/ex1의 실행 결과를 확인합니다.<br>
정상적으로 Hello World가 출력되는 것을 확인할 수 있습니다.<br>