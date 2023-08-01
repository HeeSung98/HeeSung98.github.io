---
layout: post
title: "[JavaScript] jQuery"
subtitle: posco X codingon
date: '2023-07-14 12:40:00 +0900'
category: study
tags: javascript web 포스코&nbspx&nbsp코딩온&nbsp풀스택&nbsp웹&nbsp개발자&nbsp부트캠프&nbsp8기
image:
    path: /assets/img/web/javascript/logo.png
---

jQuery를 사용해 자바스크립트를 다뤄봅시다.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

jQuery란 자바스크립트 언어를 간편하게 사용할 수 있도록 단순화 시킨 오픈 소스 기반의 라이브러리입니다.<br>
jQuery를 사용하면 DOM을 쉽게 다룰 수 있고 같은 동작도 조금 더 짧게 표현할 수 있는 장점이 있습니다.<br>

---
<br>

# 1. CDN을 통한 jQuery 불러오기
---
<br>

![1](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/1.png)
<br>

jQuery를 사용하기 위해선 jQuery 라이브러리를 불러와야 합니다.<br>
위 홈페이지에서 원하는 버전의 CDN을 클릭할 경우 위와 같이 script를 확인할 수 있습니다. 해당 script를 헤더에 작성해 jQuery를 불러올 수 있습니다.<br>

# 2. \$()
---
<br>

![2](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/2.png)
<br>

jQuery는 \$()를 사용해 원하는 요소를 가져올 수 있습니다.<br>
querySelector와 유사하게 class를 가져고자 할 때는 '.'을, id를 가져오고자 할 때는 '#'을 사용해 요소를 가져옵니다.<br>


# 3. \$().val()
---
<br>

![3](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/3.png)
<br>

jQuery에서는 val()을 사용해 불러온 요소의 value값을 가져오거나 수정할 수 있습니다.<br>
위 그림을 살펴보면 두 input의 value가 모두 '이름을 입력하세요' 였으나 #inputEmail의 value가 '\$().val()'을 통해 'e-mail을 입력하세요'로 바뀐 것을 확인할 수 있습니다.<br>

# 4. \$().attr()
---
<br>

![4](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/4.png)
<br>

요소의 속성을 변경할 때 '\$().attr()'를 사용해 변경할 수 있습니다.<br>
위 그림에서 #inputEmail의 스타일 속성이 '\$().attr()'를 통해 변경된 것을 확인할 수 있습니다.<br>


# 5. \$().text()
---
<br>

![5](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/5.png)
<br>

요소의 텍스트를 변경할 때 '\$().text()'를 사용해 변경할 수 있습니다.<br>
위 그림에서 .span1의 텍스트가 '\$().text()'를 통해 변경된 것을 확인할 수 있습니다.<br>

# 6. \$().html()
---
<br>

![6](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/6.png)
<br>

'\$().html()'을 사용해 요소 내부에 원하는 태그를 삽입할 수 있습니다.<br>

# 7. \$().append()
---
<br>

![7](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/7.png)
<br>

'\$().append()'를 사용해 자식 요소를 추가할 수 있습니다. 이 때 prepend()의 경우 자식 요소를 선택자의 앞에 추가합니다.<br>
또한 before()와 after()가 존재하는데 이들은 형제 요소로 추가합니다. 그림을 살펴보면 /<ul/>의 위 아래로 형제 요소들이 추가된 것을 확인할 수 있습니다.<br>


# 8. \$().addClass()
---
<br>

![8](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/8.png)
<br>

선택한 요소에 클래스를 추가하고 싶을 때 '\$().addClass()'를 사용할 수 있습니다.<br>
또한 remove()를 사용해 클래스를 제거할 수 있고 hasClass()를 사용해 클래스의 존재 유무를 확인한 뒤 없을 경우 추가할 수 있습니다. toggleClass()를 통해 토글기능 역시 사용할 수 있습니다.<br>


# 9. document.ready()
---
<br>

![9](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/9.png)
<br>

jQuery에는 ready() 메소드가 존재합니다. ready()를 사용해 문서의 로딩이 모두 끝났을 때 실행되는 이벤트를 지정할 수 있습니다.<br>
위 그림을 살펴보면 맨 처음 코드가 작성되었지만 모든 log가 출력된 후 'document ready'가 출력되는 것을 확인할 수 있습니다.<br>

# 10. \$().click()
---
<br>

![10](/assets/img/web/javascript/2023-07-14-[JavaScript]_jQuery/10.png)
<br>

'\$().click()'을 사용해 마우스로 해당 요소를 클릭했을 때의 이벤트를 지정할 수 있습니다.<br>
hover(), keyup(), keydown()등 여러가지 기능이 존재하며 해당 이름에 해당하는 동작을 수행할 때 이벤트가 발생합니다.<br>
