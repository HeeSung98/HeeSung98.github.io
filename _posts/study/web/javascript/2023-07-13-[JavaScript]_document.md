---
layout: post
title: "[JavaScript] document"
subtitle: posco X codingon 2주차 회고록
date: '2023-07-13 12:40:00 +0900'
category: study
tags: javascript web 포스코&nbspx&nbsp코딩온&nbsp풀스택&nbsp웹&nbsp개발자&nbsp부트캠프&nbsp8기
image:
    path: /assets/img/web/javascript/logo.png
---

document를 통해 요소를 다루는 법에 대해 알아봅시다.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

HTML 문서는 요소의 집합입니다. 각각의 node와 object의 집합으로 문서를 표현하고 이러한 node와 object에 접근하여 문서 구조 / 스타일 / 내용 등을 변형할 수 있습니다. 이를 DOM(Document Object Model)이라고 합니다.<br>
document는 웹 페이지에 존재하는 HTML 요소에 접근하여 행동하고자 할 때 사용하는 객체입니다.<br>
DOM을 통해 HTML의 모든 요소와 속성, CSS를 추가하거나 변경할 수 있습니다.<br>

---
<br>

# 1. getElementBy__()
---
<br>

![1](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/1.png)
<br>

HTML 내에서 document를 사용해 요소를 선택하는 방법은 여러가지가 존재합니다.<br>
document를 사용할 땐 위의 그림과 같이 'document.내장객체'와 같은 방법으로 사용할 수 있습니다.
ID를 통해 요소를 선택할 때는 getElementById(), Class를 통해 요소를 선택할 때는 getElementByClassName(), 태그를 통해 요소를 선택할 때는 getElementByTagName(), name을 통해 요소를 선택할 때는 getElementByName()을 사용할 수 있습니다.<br>
또한 querySelector()와 querySelectorAll()을 사용해 CSS를 통해서도 선택할 수 있습니다.<br>

# 2. querySelector()
---
<br>

![2](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/2.png)
<br>




# 3. classList
---
<br>

![3](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/3.png)
<br>



# 4. setAttribute()
---
<br>

![4](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/4.png)
<br>




# 5. createElement()
---
<br>

![5](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/5.png)
<br>



# 6. addEventListener()
---
<br>

![6](/assets/img/web/spring/2023-04-24-[Spring]_파일_업로드/6.png)
<br>


