---
layout: post
title: "[Spring] Thymeleaf의 부트스트랩 템플릿 적용하기"
subtitle: Spring
date: '2023-03-19 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

`Thymeleaf`의 `부트스트랩 탬플릿`을 적용해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

부트스트랩 탬플릿을 적용해봅시다.<br>

---
<br>

# 1. 부트스트랩 템플릿 다운로드
---
<br>

![1](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/1.PNG)
<br>

이번 실습에서 사용할 부트스트랩 템플릿은 'https://startbootstrap.com/templates/simple—sidebar/' 에서 다운받을 수 있지만 제가 실습을 위해 다운받은 결과 폴더의 내용물이 전부 존재하지 않았습니다. 따라서 추후에 깃허브 링크를 올려 공유할 수 있도록 하겠습니다.<br>

# 2. basic.html 작성
---
<br>

![2](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/2.PNG)
<br>

먼저 다운받은 파일을 static 폴더 내로 복사합니다.<br>
layout 폴더에 basic.html 파일을 추가하고 static 폴더 내의 index.html의 내용을 그대로 옮겨줍니다.

# 3. basic.html 수정 1
---
<br>

![3](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/3.PNG)
<br>

먼저 상단에 Thymeleaf와 관련된 설정을 추가합니다.<br>
th:block을 이용해 fragment를 지정하고 content라는 파라미터를 전달받을 수 있는 구조로 작성합니다.<br>
Thmeleaf의 링크로 CSS 파일의 링크나 자바스크립트 파일의 링크를 처리합니다.<br>
thblock을 닫아줍니다.<br>


# 4. basic.html 수정 2
---
<br>

![4](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/4.PNG)
<br>

파라미터로 전송돼 출력되는 부분인 container-fluid 부분을 수정합니다.<br>
파라미터로 전송되는 content를 출력하도록 위의 그림과 같이 수정합니다.<br>

# 5. exSidebar.html 작성
---
<br>

![5](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/5.PNG)
<br>

templates/sample 폴더에 exSidbar.html 파일을 추가한 뒤 위의 코드와 같이 작성합니다.<br>
앞선 실슾을 통해 basic.html에 th:fragment='content'를 전송하는 내용임을 알 수 있습니다.<br>

# 6. exSidebar.html 실행 결과
---
<br>

![6](/assets/img/web/spring/2023-03-19-[Spring]_Thymeleaf의_부트스트랩_템플릿_적용하기/6.PNG)
<br>

실행 결과 레이아웃이 유지되며 exSidebar.html의 내용을 출력하고 있는 것을 알 수 있습니다.<br>