---
layout: post
title: "[JavaScript] 동기 / 비동기 처리"
subtitle: posco X codingon
date: '2023-07-29 12:40:00 +0900'
category: study
tags: javascript web 포스코&nbspx&nbsp코딩온&nbsp풀스택&nbsp웹&nbsp개발자&nbsp부트캠프&nbsp8기
image:
    path: /assets/img/web/javascript/logo.png
---

JavaScript의 동기 처리 방식과 비동기 처리 방식에 대해 살펴봅니다.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

자바스크립트는 싱글 스레드 언어이지만 기본적으로 함수에 delay가 존재할 경우 진행을 멈추고 callback queue로 보낸 뒤 바로 다음 코드를 실행합니다. 이처럼 특정 코드의 연산이 끝날 때 까지 코드의 실행을 멈추지 않고 다음 코드를 실행하는 것을 비동기 처리라고 합니다.<br>
만약 서버로 데이터를 요청하는 코드를 작성했을 때 서버로부터의 응답이 늦게될 경우 이는 큰 성능저하를 야기할 수 있습니다. 따라서 실행중이던 코드를 멈추고 다른 코드를 실행할 수 있는 비동기 처리의 사용은 필수적입니다.<br>
하지만 항상 비동기 처리만을 사용하는 것은 아닙니다. 함수에 delay가 존재하더라도 바로 넘어가는 것이 아닌 대기 후 넘어가기를 원하는 경우는 분명 존재합니다. 이렇게 함수가 종료할 때 까지 기다린 후 다음 코드로 넘어가는 것을 동기 처리라고 합니다.<br>
기본적으로 비동기 처리를 수행하기 때문에 어떻게 동기 처리로 코드를 작성하는지 살펴보겠습니다.<br>

---
<br>

# 1. setTimeout()
---
<br>

![1](/assets/img/web/javascript/2023-07-29-[JavaScript]_동기_비동기_처리/1.png)
<br>

먼저 setTimeout()입니다. 이 메소드는 파라미터로 함수와 기다릴 시간을 입력받습니다.<br>
위 그림을 살펴보면 goMart(), pickDrink(), pay() 순으로 함수가 실행됩니다. 자바스크립트는 기본적으로 비동기 처리를 수행하기 때문에 pickDrink()를 기다리는 동안 코드가 멈추는 것이 아닌 pay(product, price)를 실행한 뒤 딜레이가 끝나고 product, price에 값을 할당하기 때문에 undefined가 출력되는 것을 확인할 수 있습니다.<br>

# 2. callback function
---
<br>

![2](/assets/img/web/javascript/2023-07-29-[JavaScript]_동기_비동기_처리/2.png)
<br>

비동기식으로 처리되는 것이 아닌 동기식으로 처리하고자 할 때 callback function을 사용할 수 있습니다. 위의 코드는 1번을 콜백형식으로 작성해 동기식으로 처리하는 코드입니다.<br>
callback function을 사용하는 방법은 함수의 맨 마지막 매개변수로 함수를 받는 것입니다. 위의 코드를 살펴보면 pickDrink() 함수에 callback이라는 매개변수를 작성하였고 이는 내부에서 함수로 동작하도록 사용되었습니다. goMart()가 실행된 뒤 pay()는 pickDrink()의 매개변수로 사용되었고 값을 전부 할당한 뒤 pay()가 setTimeout() 내부에서 실행되는 것을 확인할 수 있습니다.<br>
이 때 매개변수로 함수를 넘길 때 괄호를 작성지 않고 함수명만 작성하는 점을 유의해야 합니다.<br>


# 3. callback function의 단점
---
<br>

![3](/assets/img/web/javascript/2023-07-29-[JavaScript]_동기_비동기_처리/3.png)
<br>

callback function을 여러번 사용할 경우 위의 그림과 같이 코드의 가독성이 크게 떨어지는 단점이 있습니다.<br>
이런 단점을 극복하기 위해 Promise 객체가 등장하였습니다.<br>


# 4. Promise
---
<br>

![4](/assets/img/web/javascript/2023-07-29-[JavaScript]_동기_비동기_처리/4.png)
<br>

Promise란 비동기 함수를 동기 처리하기 위해 만들어진 객체입니다. Promise는 함수에 대해 성공과 실패를 반환합니다. 비동기 작업이 완료된 후 다음 작업을 연결해 동기 처리할 수 있습니다.<br>
위 그림은 3번을 Promise를 사용해 작성한 코드입니다. changeColor()는 color를 매개변수로 받고 Promise 객체를 생성합니다. 그 후 배경을 color로 변경한 뒤 정상적으로 모두 실행이 되었다면 resolve()를 실행하고 color를 반환합니다. 만약 에러가 발생할 경우 reject() 내부의 값을 반환합니다.<br>
changColor('red')가 반환한 red는 resultRed에 담겼습니다. 하지만 이 함수는 새로운 색을 매개변수로 사용해야 하기 때문에 리턴값을 담은 result___는 의미가 없지만 단순히 표현을 위해 작성하였습니다.<br>


# 5. async / await
---
<br>

![5](/assets/img/web/javascript/2023-07-29-[JavaScript]_동기_비동기_처리/5.png)
<br>

이러한 Promise 객체를 좀 더 이해하기 쉽고 편하게 작성하기 위해 async / await가 등장했습니다.<br>
위의 코드는 1번과 2번을 async / await를 통해 작성한 코드입니다.<br>
pickDrink()는 Promise 객체를 사용해 동일하게 작성합니다. 다른 점은 코드를 실행하는 excute()가 작성되었고 이 함수의 선언부 앞에 async가 작성되었습니다. excute()는 goMart(), pickDrink(), pay()를 순서대로 실행합니다.<br>
이때 pickDrink() 앞에 await가 작성되었는데 이는 pickDrink()의 Promise가 전부 처리될 때 까지 대기한다는 뜻입니다. pickDrink()가 모두 끝나고 money값에 따라 resolve()와 reject()가 실행됩니다. money가 충분한 경우 flag를 1로 바꾼 뒤 함수를 종료하고, 부족한 경우 reject()에 값을 담아 반환한 뒤 해당 값을 log로 출력합니다. 만약 flag가 1일 경우에만 pay()가 실행됩니다.<br>
