---
layout: post
title: "[Spring] JpaRepository 및 테스트 코드를 통한 CRUD"
subtitle: Spring
date: '2023-02-10 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

`Intellij IDE`와 `Spring boot`로 프로젝트를 생성하고 실행해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

스프링 부트란 스프링 프레임워크를 이용해서 웹 어플리케이션을 더 간단하고 빠르게 개발할 수 있는 도구입니다.<br>
스프링 부트를 이용하는 개발 도구는 여러 가지가 있지만 가장 널리 사용되고 있는 Intellij Ultimate버전을 사용하도록 하겠습니다.<br>
---
<br>

![1](/assets/img/study_Web/spring/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/intellij.png){: width="500" height="500"}

`Intellij`는 JetBrains사에서 제작한 상용 자바 통합 개발 환경입니다.
<br>
Intellij는 Ultimate와 Community 두 가지 버전이 존재하는데 Ultimate는 GUI 환경에서 스프링 부트 개발 환경을 이용할 수 있고, 자동 완성 등의 도움을 주기는 하지만 기본적으로 30일 제한이 있고, 1년 단위의 라이선스 비용이 부담스럽다는 단점이 있습니다.
<br>
하지만 학교 메일 계정을 갖고 있는 분들은 메일 인증을 통해서 1년 단위의 무료 사용이 가능합니다.

<br>

# 1. 새 프로젝트 만들기
---
<br>