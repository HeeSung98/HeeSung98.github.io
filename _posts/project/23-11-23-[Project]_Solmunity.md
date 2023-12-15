---
layout: post
title: "[Project] Solmunity"
subtitle: sample
date: '2023-11-23 12:40:00 +0900'
category: project
tags: node.js web project python
image:
    path: /assets/img/project/23-11-23-[Project]_Solmunity/logo.png
---

솔리디티 개발자를 위한 코드의 제어 흐름 그래프를 제공하는 웹 커뮤니티 애플리케이션입니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

하나의 파일에 프로젝트의 모든 내용을 담을 경우 유지 보수가 힘들어지고 코드의 가독성이 크게 떨어집니다.<br>
때문에 MVC 디자인 패턴에 맞게 코드를 분리하여 작성하고자 합니다.<br>

---
<br>

# 1. MVC 패턴이란?
---
<br>

![1](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/1.png)
<br>

MVC란 Model - View - Controller의 앞글자를 따온 단어입니다. 크게 Model, View, Controller로 역할을 나눠 파일을 분리하도록 코드를 작성하는 것을 MVC 디자인 패턴이라고 합니다.<br>
Model은 데이터와 비지니스 로직을 관리하고 View는 레이아웃과 화면을 처리합니다. Controller는 모델과 뷰 사이의 명령을 라우팅합니다.<br>
이러한 "separation of concerns"는 더 나은 분업을 가능하게 하고 유지 보수를 용이하게 합니다.<br>
이제 위 그림과 같이 node.js에서 MVC 패턴으로 프로젝트를 생성해 보겠습니다.<br>


# 2. package.json
---
<br>

![2](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/2.png)
<br>

이번 프로젝트에서 사용하는 모듈과 버전은 위와 같습니다.<br>

# 3. executable code - app.js
---
<br>

![3](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/3.png)
<br>

프로젝트의 실행파일은 위와 같습니다.<br>
기존의 방식처럼 app.js나 index.js에서 url의 매핑과 구현을 작성하는 것이 아닌 indexRouter로 요청을 넘기는 방식으로 작성된 것을 확인할 수 있습니다.<br>
indexRouter는 동일한 패키지에 routes 패키지를 생성한 뒤 index.js 파일을 불러옵니다. 경로에는 './routes' 만 적혀있지만 파일명이 index인 파일을 자동으로 불러오기 때문에 './routes/index'와 동일하게 동작합니다.<br>
그렇다면 이제 url에 대한 처리를 작성할 ㅍ


# 4. router - index.js
---
<br>

![4](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/4.png)
<br>




# 5. 
---
<br>

![5](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/5.png)
<br>



# 6. 
---
<br>

![6](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/6.png)
<br>



# 7. 
---
<br>

![7](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/7.png)
<br>



# 8. 
---
<br>

![8](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/8.png)
<br>




# 9. 
---
<br>

![9](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/9.png)
<br>



# 10. 
---
<br>

![10](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/10.png)
<br>



# 11. 
---
<br>

![11](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/11.png)
<br>



# 12. 
---
<br>

![12](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/12.png)
<br>



# 13. 
---
<br>

![13](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/13.png)
<br>



# 14. 
---
<br>

![14](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/14.png)
<br>



# 15. 
---
<br>

![15](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/15.png)
<br>



# 16. 
---
<br>

![16](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/16.png)
<br>



# 17. 
---
<br>

![17](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/17.png)
<br>



# 18. 
---
<br>

![18](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/18.png)
<br>



# 19. 
---
<br>

![19](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/19.png)
<br>



# 20. 
---
<br>

![20](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/20.png)
<br>



# 21. 
---
<br>

![21](/assets/img/web/nodejs/2023-08-05-[node.js]_MVC_패턴_프로젝트/21.png)
<br>

