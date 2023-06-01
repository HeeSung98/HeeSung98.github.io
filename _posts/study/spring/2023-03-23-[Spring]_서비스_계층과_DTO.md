---
layout: post
title: "[Spring] 서비스 계층과 DTO"
subtitle: Spring
date: '2023-03-23 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/study_Web/spring/logo.png
---

데이터 저장 계층 바깥에서 `Entity` 대신 `DTO`를 사용해봅시다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>
이전의 방식은 엔티티를 통해 쿼리를 작성하거나 테스트 하였지만 실제 프로젝트를 작성할 때 데이터 저장 계층 바깥쪽에서 엔티티를 사용하는 것 보단 DTO를 사용하는 방식을 권장합니다.<br>
DTO는 순수하게 데이터를 담고 있으며 데이터의 전달을 목적으로 합니다. 또한 읽기 쓰기가 허용되고 일회성으로 사용되는 성격이 강합니다. Entity는 실제 데이터베이스와 관련이 있고, 내부적으로 엔티티 매니저가 관리하는 객체입니다. DTO의 일회성과는 느낌이 많이 다릅니다.<br>
DTO를 사용하는 경우 가장 큰 단점은 Entity와 유사한 코드를 중복으로 개발한다는 점과 Entity를 DTO로, DTO를 Entity로 변환하는 과정이 필요하다는 것입니다. 하지만 DTO를 사용하면 엔티티 객체의 범위를 한정 지을 수 있기 떄문에 좀 더 안전한 코드를 작성할 수 있고, 화면과 데이터를 분리하려는 취지에 더 적합하다는 장점이 있습니다.<br>

---
<br>

# 1. GuestbookDTO 작성
---
<br>

![1](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/1.PNG)
<br>

프로젝트 내에 dto 패키지와 service 패키지를 추가합니다. dto 패키지에는 서비스 계층에서 파라미터와 리턴 타입으로 사용되는 GuestbookDTO 클래스를 위의 그림과 같이 작성합니다.<br>
GuestbookDTO는 엔티티 클래스인 Guestbook의 컬럼을 변수로 갖고 있습니다. 이러한 필드는 @Data를 통해 getter/setter로 자유롭게 변경할 수 있게 구성합니다.<br>
서비스 계층에서 GuestbookDTO를 통해 필요한 내용을 전달하도록 GuestbookService 인터페이스와 GuestbookServiceImpl 클래스를 작성합니다.<br>

# 2. GuestbookService 인터페이스 작성
---
<br>

![2](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/2.PNG)
<br>

GuestbookService 인터페이스는 service 패키지를 생성한 뒤 작성하고 코드는 위의 그림과 같습니다.<br>

# 3. GuestbookServiceImpl 클래스 작성
---
<br>

![3](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/3.PNG)
<br>

GuestbookServiceImpl 클래스는 @Service 어노테이션을 통해 스프링에서 빈으로 처리되게 합니다.<br>

# 4. dtoToEntity 메소드 작성
---
<br>

![4](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/4.PNG)
<br>

서비스 계층은 파라미터를 DTO 타입으로 사용합니다. 이를 JPA로 처리하기 위해서는 DTO를 엔티티 타입의 객체로 변환해야 합니다. 이러한 기능을 수행할 dtoToEntity 메소드를 default 메소드로 GuestbookService 인터페이스에 작성합니다.<br>
dtoToEntity는 엔티티를 리턴하는데 이 엔티티는 DTO를 매개변수로 받아 dto.get을 통해 엔티티를 빌드합니다.<br>


# 5. dtoToEntity의 활용
---
<br>

![5](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/5.PNG)
<br>

4번에서 구현한 dtoTOEntity를 GuestbookSErviceImpl 클래스에서 활용해보겠습니다.<br>
guestbookDTO 타입의 dto를 매개변수로 받은 뒤 dtoToEntity에 매개변수로 넣습니다. 리턴값은 Guestbook 타입의 엔티티인 entity로 받는 것을 확인할 수 있습니다.<br>

# 6. 서비스 계층의 테스트
---
<br>

![6](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/6.PNG)
<br>

작성된 GuestbookService에 대한 테스트 작업을 수행하기 위해 test 폴더에 service 패키지를 추가한 뒤 위의 그림과 같은 코드를 작성합니다.<br>
testRegister()의 실행 결과 데이터베이스에는 저장되지 않았지만 GuestbookDTO가 Guestbook 타입의 엔티티로 변환된 것을 확인할 수 있습니다.<br>


# 7. 데이터베이스에 저장되도록 수정
---
<br>

![7](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/7.PNG)
<br>

변환이 무사히 성공했기 때문에 GuestbookServiceImpl 클래스를 수정해 실제로 데이터베이스에 저장되도록 수정하겠습니다.<br>
GuestbookServiceImpl 클래스는 JPA 처리를 위해 GuestbookRepository를 주입합니다. 이때 `@RequiredArgsConstructor`를 이용하면 자동으로 주입해줍니다.<br>
register() 내부에는 save()를 통해 저장하고 해당 엔티티의 gno값을 반환하도록 수정합니다.<br>

# 8. 데이터베이스에 저장되도록 수정 결과
---
<br>

![8](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/8.PNG)
<br>

테스트 코드 testRegister()를 다시 실행한 뒤 스택트레이서를 살펴보면 Hibernate 문구가 출력되며 추가된 데이터의 gno인 301이 출력되는 것을 확인할 수 있습니다.<br>

# 9. DTO가 데이터베이스에 저장된 결과
---
<br>

![9](/assets/img/study_Web/spring/2023-03-23-[Spring]_서비스_계층과_DTO/9.PNG)
<br>

MySQL Workbench에서도 살펴본 결과 DTO를 통해 만들어진 데이터가 정상적으로 저장된 것을 확인할 수 있습니다.<br>