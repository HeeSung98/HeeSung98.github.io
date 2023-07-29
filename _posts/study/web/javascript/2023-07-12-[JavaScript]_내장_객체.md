---
layout: post
title: "[JavaScript] 내장 객체"
subtitle: posco X codingon 2주차 회고록
date: '2023-07-12 12:40:00 +0900'
category: study
tags: javascript web 포스코&nbspx&nbsp코딩온&nbsp풀스택&nbsp웹&nbsp개발자&nbsp부트캠프&nbsp8기
image:
    path: /assets/img/web/javascript/logo.png
---

자바스크립트의 내장 객체들을 살펴봅니다.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>



---
<br>

# 1. String
---
<br>

![1](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/a.png)
<br>

.length: 해당 객체의 길이를 반환합니다.<br>
.toUpperCase(): 해당 객체를 전부 대문자로 변환합니다.<br>
.indexOf(): 해당 객체에서 파라미터로 받은 값이랑 처음으로 일치하는 글자의 위치를 반환합니다.<br>
.lastIndexOf(): indexOf()가 처음부터 탐색해 일치하는 글자를 반환한다면 lastIndexOf()의 경우 마지막부터 탐색해 처음으로 일치하는 글자의 인덱스를 반환합니다.<br>
.slice(): 파라미터로 지정한 범위만큼 잘라낸 뒤 반환합니다.<br>
.replace(): 첫 파라미터의 글자를 탐색한 뒤 해당 글자를 두 번째 파라미터로 바꿉니다.<br>
.repeat(): 파라미터의 수 만큼 반복합니다.<br>
.split(): 파라미터를 지정하면 해당 파라미터를 기준으로 문자열을 나눕니다. 지정하지 않을 시 ,를 통해 객체를 한 글자씩 분리합니다.<br>
.trim(): 처음부분과 끝부분에 공백이 존재한다면 해당 공백을 제거합니다.<br>

# 2. Array
---
<br>

![2](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/b.png)
<br>

.length: 해당 배열의 길이를 반환합니다.<br>
.push(): 파라미터를 해당 배열 맨 끝에 삽입한 후 해당 배열의 길이를 반환합니다.<br>
.pop(): 해당 배열의 맨 끝의 값을 삭제한 후 반환합니다.<br>
.unshift(): 파라미터를 해당 배열 맨 앞에 삽입한 후 해당 배열의 길이를 반환합니다.<br>
.shift(): 해당 배열의 맨 앞의 값을 삭제한 후 반환합니다.<br>
.indexOf(): 해당 배열에서 파라미터로 받은 값이랑 처음으로 일치하는 요소의 인덱스를 반환합니다. 두 번째 파라미터가 존재할 경우 해당 인덱스부터 탐색을 시작합니다.<br>
.include(): 해당 배열에서 파라미터로 받은 값과 일치하는 요소가 존재할 경우 True를, 아닐 경우 False를 반환합니다.<br>
.reverse(): 해당 배열의 요소의 순서를 뒤집습니다.<br>
.join(): 해당 배열을 합쳐 문자 객체로 만듭니다. 파라미터를 입력하면 배열의 원소를 합칠 때 해당 파라미터가 중간에 사용됩니다.<br>


# 3. String \<--\> Array
---
<br>

![3](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/c.png)
<br>

split()과 join()을 사용해 문자 객체를 배열 객체로, 배열 객체를 문자 객체로 변환할 수 있습니다.<br>
또한 메소드를 한 라인에 연결해 사용할 수 있고 이를 메소드 체이닝이라고 합니다.<br>


# 4. Array 탐색
---
<br>

![4](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/d.png)
<br>

for문과 .filter()를 사용해 배열의 요소를 탐색할 수 있습니다.<br>


# 5. Date
---
<br>

![5](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/e.png)
<br>

Date는 자바스크립트에서 날짜를 다룰 때 사용하는 객체입니다.<br>
Date 객체는 1970년 1월 1일 0시 0분 0초를 기준일로 사용하고 있습니다. Date.now()와 .getTime()을 사용할 경우 기준일로부터 지난 시간을 밀리세컨드 단위로 반환합니다.<br>

# 6. Math
---
<br>

![6](/assets/img/web/javascript/2023-07-12-[JavaScript]_내장_객체/f.png)
<br>

Math는 자바스크립트에서 수학을 다룰 때 사용하는 객체입니다.<br>
Math 객체를 사용해 random한 값을 다룰 수 있습니다.<br>
