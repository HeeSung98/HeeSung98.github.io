---
layout: post
title: "[MariaDB] Database 한글 설정"
subtitle: Mariadb
date: '2023-04-12 11:40:00 +0900'
category: study
tags: mariadb database
image:
    path: /assets/img/database/mariadb/logo.png
---

데이터베이스에서 한글을 사용할 수 있도록 설정해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}


# 1.
---
<br>

![1](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/1.png)<br>

데이터베이스에서 한글을 사용할 수 있도록 하는 SQL문은 위의 그림과 같습니다. ALTER를 통해 charset 값을 utf8로 변경하는 쿼리입니다.<br>
하지만 위 그림과 같이 FK를 사용해 다른 테이블을 참조하는 테이블일 경우 에러가 발생합니다.<br>

# 2.
---
<br>

![2](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/2.png)<br>

이때 SET FOREIGN_KEY_CHECKS = 0;를 사용하면 FK의 제약조건을 끄도록 할 수 있습니다.<br> 제약조건을 끈다면 에러를 무시하고 진행할 수 있습니다.<br>

# 3.
---
<br>

![3](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/3.png)<br>

다시 ALTER문을 실행한 결과 처리가 완료된 것을 확인할 수 있습니다.<br>

# 4.
---
<br>

![4](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/4.png)<br>

그 후 SET FOREIGN_KEY_CHECKS = 1;을 통해 FK의 제약조건을 다시 켜줍니다.<br>

# 5.
---
<br>

![5](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/5.png)<br>

작성중인 board 프로젝트에서 한글 게시글을 작성해보겠습니다.<br>

# 6.
---
<br>

![6](/assets/img/database/mariadb/2023-04-10-[MariaDB]_Database_한글_설정/6.png)<br>

정상적으로 한글 게시글이 작성된 것을 확인할 수 있습니다.<br>
