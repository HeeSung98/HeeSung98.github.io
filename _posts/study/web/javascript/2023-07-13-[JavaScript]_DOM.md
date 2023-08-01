---
layout: post
title: "[JavaScript] document"
subtitle: posco X codingon
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

![1](/assets/img/web/spring/2023-07-13-[JavaScript]_document/1.png)
<br>

HTML 내에서 document를 사용해 요소를 선택하는 방법은 여러가지가 존재합니다. 먼저 'document.내장객체'와 같은 방법으로 사용할 수 있습니다.<br>
document의 내장객체 중 getElementBy를 살펴보겠습니다.  Class를 통해 요소를 선택할 때는 getElementsByClassName(), ID를 통해 요소를 선택할 때는 getElementById(), name을 통해 요소를 선택할 때는 getElementsByName(), 태그를 통해 요소를 선택할 때는 getElementsByTagName()을 사용할 수 있습니다.<br>
각각 가져온 데이터를 살펴보면 getElementById()는 동일한 Id를 가진 하나의 객체를 불러오고 나머지는 해당되는 모든 객체를 불러온 것을 알 수 있습니다.<br>

# 2. querySelector()
---
<br>

![2](/assets/img/web/spring/2023-07-13-[JavaScript]_document/2.png)
<br>

document에는 getElementBy가 아닌 querySelector라는 객체도 존재합니다.<br>
querySelector()는 요소 선택자를 이용해 자신이 가져오고 싶은 요소를 하나 가져옵니다. getElementBy와 달리 querySelector의 경우 querySelector 하나로 id와 class, 태그와 같은 요소를 모두 불러올 수 있습니다.<br>
또한 querySelectorAll()을 사용해 모든 요소를 가져오게 할 수 있습니다.<br>


# 3. classList
---
<br>

![3](/assets/img/web/spring/2023-07-13-[JavaScript]_document/3.png)
<br>



# 4. setAttribute()
---
<br>

![4](/assets/img/web/spring/2023-07-13-[JavaScript]_document/4.png)
<br>




# 5. createElement()
---
<br>

![5](/assets/img/web/spring/2023-07-13-[JavaScript]_document/5.png)
<br>



# 6. addEventListener()
---
<br>

![6](/assets/img/web/spring/2023-07-13-[JavaScript]_document/6.png)
<br>


