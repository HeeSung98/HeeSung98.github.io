---
layout: post
title: "[Spring] Spring boot로 프로젝트 생성하기"
subtitle: Spring
date: '2023-02-05 11:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/logo.png
---

`Intellij IDE`와 `Spring boot`로 프로젝트를 생성하고 실행해봅시다.

<br>
<hr/>
<br>

스프링 부트란 스프링 프레임워크를 이용해서 웹 어플리케이션을 더 간단하고 빠르게 개발할 수 있는 도구입니다.<br>
스프링 부트를 이용하는 개발 도구는 여러 가지가 있지만 가장 널리 사용되고 있는 Intellij Ultimate버전을 사용하도록 하겠습니다.

<br>
<hr/>
<br>

![1](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/intellij.png)

`Intellij`는 JetBrains사에서 제작한 상용 자바 통합 개발 환경입니다.
<br>
Intellij는 Ultimate와 Community 두 가지 버전이 존재하는데 Ultimate는 GUI 환경에서 스프링 부트 개발 환경을 이용할 수 있고, 자동 완성 등의 도움을 주기는 하지만 기본적으로 30일 제한이 있고, 1년 단위의 라이선스 비용이 부담스럽다는 단점이 있습니다.
<br>
하지만 학교 메일 계정을 갖고 있는 분들은 메일 인증을 통해서 1년 단위의 무료 사용이 가능합니다.

<br>
<hr/>
<br>

## 1. 새 프로젝트 만들기
<br>


이제 Intellij Ultimate를 사용해 새로운 Spring boot 프로젝트를 생성해보겠습니다.
<br>
처음 시작하는 화면에서 'Create New Project'를 선택해서 프로젝트를 생성할 수 있습니다. 이 때 프로젝트 생성 메뉴에서 'Spring Initializr' 메뉴를 선택하고 필요한 정보를 입력합니다.
<br>

![2](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p1.png)
<br>
제가 입력한 프로젝트 정보는 위와 같습니다.<br>
Java 버전은 현재 자신의 버전에 맞게 선택하되, 현재 설치된 JDK 버전과 동일하거나 낮은 버전을 선택합니다.

<br>
<hr/>
<br>

## 2. 의존성 선택
<br>

![3](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p2.png)
<br>

Next 버튼을 누른다면 그림과 같은 의존성 선택 화면으로 넘어갑니다. <br>
저는 Spring Boot DevTools, Lombok, Spring Web을 검색한 후 체크하겠습니다.

<br>
<hr/>
<br>

## 3. 생성된 스프링 프로젝트 실행해 보기
<br>

![4](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p3.png)
<br>
작성된 프로젝트가 정상적으로 실행 가능한지 확인하기 위해서 Ex1Application 파일의 메소드를 실행해보겠습니다.

<br>
<hr/>
<br>

## 4. 메소드의 실행 결과
<br>

![5](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p4.png)
<br>
메서드의 실행 과정에서는 다음과 같은 스프링 부트의 배너가 출력되면서 프로젝트가 실행됩니다. 기본적으로 8080포트를 사용하며 성공적으로 실행된 것을 확인할 수 있습니다.

<br>
<hr/>
<br>

## 5. 테스트 코드의 실행
<br>

![6](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p5.png)
<br>
생성된 스프링 부트 프로젝트의 경우 이미 테스트 환경이 갖춰져 있기 때문에 별도의 설정 없이 프로젝트를 실행할 수 있습니다. <br>
작성되어 있는 Ex1ApplicationTests 파일에서 @Test가 있는 메소드를 선택해서 실행해볼 수 있습니다.<br>
테스트 코드가 무엇인지는 별도의 글을 통해 살펴보겠습니다.

<br>
<hr/>
<br>

## 6. 간단한 컨트롤러 실습
<br>
스프링으로 컨트롤러를 사용하기 위해서는 많은 설정이 필요하지만, 스프링 부트는 자동으로 설정되는 부분이 많습니다. 2번에서 추가한 'Spring Web' 의존성이 다양한 라이브러리를 자동으로 추가해주기 때문입니다. <br>

<br>

![7](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p6.png)
<br>

위와 같은 SampleController는 @RestController를 이용해서 별도의 화면 없이 데이터를 전송하고자 합니다. <br>
hello()는 @GetMapping을 이용해서 브라우저의 주소창에서 호출이 가능하도록 설정합니다.

<br>
<hr/>
<br>

## 7. 컨트롤러 호출하기
<br>
프로젝트 내에 있는 Ex1Application 클래스의 main()을 실행하고 브라우저로 'http://localhost:8080/hello'를 호출합니다.

<br>

![78](/assets/img/study_Web/2023-02-05_[Spring]_Spring_boot로_프로젝트_생성하기/p7.png)
<br>

컨트롤러에 작성된 {"Hello", "World"}가 localhost:8080/hello에서 출력되는 것을 확인할 수 있습니다.