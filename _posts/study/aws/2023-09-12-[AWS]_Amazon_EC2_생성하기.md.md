---
layout: post
title: "[node.js] MVC 패턴 프로젝트"
subtitle: sample
date: '2023-09-12 12:40:00 +0900'
category: study
tags: node.js web 포스코&nbspx&nbsp코딩온&nbsp풀스택&nbsp웹&nbsp개발자&nbsp부트캠프&nbsp8기
image:
    path: /assets/img/aws/logo.png
---

`Amazon Web Service`에서 제공하는 `Amazon EC2`서버를 생성해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

EC2는 좋아

---
<br>

# 1. MVC 패턴이란?
---
<br>

![1](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/1.png)
<br>

MVC란 Model - View - Controller의 앞글자를 따온 단어입니다. 크게 Model, View, Controller로 역할을 나눠 파일을 분리하도록 코드를 작성하는 것을 MVC 디자인 패턴이라고 합니다.<br>
Model은 데이터와 비지니스 로직을 관리하고 View는 레이아웃과 화면을 처리합니다. Controller는 모델과 뷰 사이의 명령을 라우팅합니다.<br>
이러한 "separation of concerns"는 더 나은 분업을 가능하게 하고 유지 보수를 용이하게 합니다.<br>
이제 위 그림과 같이 node.js에서 MVC 패턴으로 프로젝트를 생성해 보겠습니다.<br>


# 2. package.json
---
<br>

![2](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/2.png)
<br>

이번 프로젝트에서 사용하는 모듈과 버전은 위와 같습니다.<br>

# 3. executable code - app.js
---
<br>

![3](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/3.png)
<br>

프로젝트의 실행파일은 위와 같습니다.<br>
기존의 방식처럼 app.js나 index.js에서 url의 매핑과 구현을 작성하는 것이 아닌 indexRouter로 요청을 넘기는 방식으로 작성된 것을 확인할 수 있습니다.<br>
indexRouter는 동일한 패키지에 routes 패키지를 생성한 뒤 index.js 파일을 불러옵니다. 경로에는 './routes' 만 적혀있지만 파일명이 index인 파일을 자동으로 불러오기 때문에 './routes/index'와 동일하게 동작합니다.<br>
그렇다면 이제 url에 대한 처리를 작성할 ㅍ


# 4. router - index.js
---
<br>

![4](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/4.png)
<br>




# 5. 
---
<br>

![5](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/5.png)
<br>



# 6. 
---
<br>

![6](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/6.png)
<br>



# 7. 
---
<br>

![7](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/7.png)
<br>



# 8. 
---
<br>

![8](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/8.png)
<br>




# 9. 
---
<br>

![9](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/9.png)
<br>



# 10. 
---
<br>

![10](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/10.png)
<br>



# 11. 
---
<br>

![11](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/11.png)
<br>



# 12. 
---
<br>

![12](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/12.png)
<br>



# 13. 
---
<br>

![13](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/13.png)
<br>



# 14. 
---
<br>

![14](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/14.png)
<br>



# 15. 
---
<br>

![15](/assets/img/aws/2023-09-12-[AWS]_Amazon_EC2_생성하기/15.png)
<br>


