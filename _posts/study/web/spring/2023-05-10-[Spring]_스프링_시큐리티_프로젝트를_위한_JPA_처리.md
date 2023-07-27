---
layout: post
title: "[Spring] 스프링 시큐리티 프로젝트를 위한 JPA 처리"
subtitle: Spring
date: '2023-05-10 12:40:00 +0900'
category: study
tags: spring web
image:
    path: /assets/img/web/spring/logo.png
---

스프링 시큐리티를 활용하는 프로젝트를 위한 JPA 처리를 해봅니다.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}
<br>

프로젝트에 스프링 시큐리티를 적용하기 위해서는 당연히 이에 맞는 데이터베이스 관련 처리가 필요합니다.<br>
이번 프로젝트는 아이디 대신 이메일을 아이디로 사용해 회원을 처리합니다.<br>
회원 정보는 이메일, 패스워드, 이름, 소셜 회원 가입 여부, 등록일 및 수정일로 구성합니다. 또한 앞서 사용한 권한에 대한 처리 또한 작성합니다.<br>
스프링 시큐리티에서는 회원이나 계정에 대해서 User라는 용어를 사용하기 때문에 User라는 단어를 사용할 때는 상당히 주의해야 합니다. 회원 아이디라는 용어 대신 username이라는 단어를 사용합니다. 스프링 시큐리티에서는 username이라는 단어 자체가 회원을 구별할 수 있는 식별 데이터를 의미합니다. 즉 일반적인 id의 개념에 해당합니다.<br>
이를 인지하고 JPA의 처리를 시작합니다.<br>

---
<br>

# 1. ClubMember 생성
---
<br>

![1](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/1.png)
<br>

entity 패키지를 추가하고 BaseEntity 클래스와 ClubMember 클래스를 생성합니다.<br>
ClubMember는 여러 개의 권한을 가질 수 있어야 합니다. 일반적으로 회원의 권한은 하나만 가지는 것이 정상적이지만 한 명의 회원이 여러 권한을 가질 수 있다는 전제로 프로젝트를 구성합니다.<br>


# 2. ClubApplication - @EnableJpaAuditing 작성
---
<br>

![2](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/2.png)
<br>

BaseEntity의 사용을 위해 ClubApplication에 `@EnableJpaAuditing` 어노테이션을 추가합니다.


# 3. ClubMemberRole 생성
---
<br>

![3](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/3.png)
<br>

entity 패키지 내에 ClubMemberRole이라는 enum 타입을 생성하고 권한을 작성합니다.<br>


# 4. ClubMember - addMemberRole() 작성
---
<br>

![4](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/4.png)
<br>

ClubMember에 ClubMemberRole 타입값을 처리하기 위해 Set\<ClubMemberRole\> 타입을 추가하고, Fetch는 LAZY 타입으로 지정합니다.<br> 또한 권한을 객체의 일부로 사용하기 위해 `@ElementCollection`을 사용합니다.<br>


# 5. ER 다이어그램 확인
---
<br>

![5](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/5.png)
<br>

프로젝트를 실행한 뒤 생성된 테이블을 확인합니다.<br>



# 6. ClubMemberRepository 생성
---
<br>

![6](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/6.png)
<br>

프로젝트 내에 repository 패키지를 춛가하고, ClubMemberRepository를 생성합니다.<br>


# 7. ClubMemberTests 생성 및 ClubMemberTests - insertDummies() 작성
---
<br>

![7](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/7.png)
<br>

ClubMemberRepository를 테스트 하기 위해 ClubMemberTests를 test 패키지 내에 생성하고 insertDummies()를 작성합니다.<br>
80명은 USER, 20명은 USER 및 MANAGER, 10명은 USER 및 MANAGER 및 ADMIN의 권한을 갖도록 작성합니다.<br>


# 8. ClubMemberTests - insertDummies() 결과
---
<br>

![8](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/8m.png)
<br>

실행 후 데이터베이스에서 club_member_role_set을 확인한다면 3개의 권한을 전부 다 받은 이메일은 0, 1, 2의 Role을 전부 가지고 있는 것을 알 수 있습니다.<br>


# 9. ClubMemberRepository - findByEmail() 작성
---
<br>

![9](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/9.png)
<br>

ClubMember의 조회를 위한 findByEmail()을 작성합니다.<br>
조회는 이메일을 기준으로 하고 일반 로그인 사용자와 소셜 로그인 사용자를 구분하기 위해 별도의 메소드를 작성합니다.<br>
findByEmail()은 사용자의 이메일과 소셜로 추가된 회원 여부를 선택해서 동작하도록 작성합니다. `@EntityGraph`를 이용해 left outer join으로 ClubMemberRole이 처리될 수 있도록 합니다.<br>

# 10. ClubMemberTests - testRead() 작성 및 결과
---
<br>

![10](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/10.png)
<br>

findByEmail()을 테스트하기 위한 testRead()를 작성합니다.<br>
실행 결과 정상적으로 조회를 하며 권한 또한 가져오는 것을 확인할 수 있습니다.<br>


# 11. ClubAuthMemberDTO 생성
---
<br>

![11](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/11.png)
<br>

서론에서 말한 스프링 시큐리티의 특징을 처리하는 핵심적인 부품은 UserDetialsService입니다.<br>
UserDetailsService는 loadUserByUsername()이라는 단 하나의 메소드를 가지고 있습니다. loadUserByUsername()은 말 그대로 username이라는 회원 아이디와 같은 식별 값으로 회원 정보를 가져옵니다. 이 때 UserDetails라는 타입을 리턴하는데 이를 통해 사용자가 가지는 권한에 대한 정보 및 인증을 마무리하기 위한 패스워드 정보, 인증에 필요한 아이디와 같은 정보, 계정의 만료 여부 및 잠김 여부를 알 수 있습니다.<br>
핵심은 이러한 정보를 처리할 때 기존 DTO 클래스에 UserDetails 인터페이스를 구현하는 방법과 DTO와 같은 개념으로 별도의 클래스를 구성하고 이를 활용하는 방법 중 어떤 것을 사용하는가 입니다. 저는 후자의 방법을 사용하도록 하겠습니다.<br>
dto 패키지에 ClubAuthMemberDTO 클래스를 생성하고 User 클래스를 상속한 뒤 부모 클래스의 생성자를 호출할 수 있는 코드를 작성합니다.<br>
기존의 코드에서 엔티티 클래스와 DTO 클래스를 별도로 구성했듯이 ClubAuthMemberDTO를 생성해 활용합니다.<br>
ClubAuthMemberDTO는 DTO 역할을 수행하는 동시에 스프링 시큐리티에서 인가/인증 작업에 사용할 수 있습니다.<br>

# 12. ClubUserDetailsService 생성
---
<br>

![12](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/12.png)
<br>

ClubMember가 ClubAuthMemberDTO라는 타입으로 처리된 가장 큰 이유는 사용자의 정보를 가져오는 핵심적인 역할을 하는 UserDetialsService라는 인터페이스 때문입니다. 스프링 시큐리티의 구조에서 인증을 담당하는 AuthenticationManager는 내부적으로 UserDetailsService를 호출해 사용자의 정보를 가져옵니다. 현재 예제와 같이 JPA로 사용자의 정보를 가져오고 싶다면 이 부분을 UserDetailsService가 이용하는 구조로 작성할 필요가 있습니다.<br>
`@Service`를 사용해 자동으로 스프링에서 빈으로 처리될 수 있게 작성하고 loadUserByUsername()의 경우 별도의 처리없이 로그만을 기록하도록 작성합니다.<br>


# 13. SecurityConfig - userDetailsService() 삭제
---
<br>

![13](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/13.png)
<br>

기존에 로그인을 테스트 하기 위해 임시로 작성한 userDetailsService()를 제거합니다.<br>
제거 후 프로젝트를 시작한 후 '/sample/member'로 이동할 경우 로그인 창이 나타나게 되고 데이터베이스에 있는 실제 계정으로 로그인을 시도할 수 있으나 로그인 처리가 이루어지지 않은 상태이기 때문에 에러가 발생할 것입니다.<br>
하지만 서버에서는 정상적으로 ClubUserDetailsService가 동작하는 것을 확인할 수 있습니다.<br>

# 14. ClubUserDetailsService - loadUserByUsername() 수정
---
<br>

![14](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/14.png)
<br>

로그인 처리를 위해 ClubUserDetailsService의 loadUserByUsername()에 처리 과정을 작성합니다.<br>
ClubMemberRepository를 주입받은 뒤 findByEmail()을 사용해 일반 로그인에 대한 계정 정보를 불러옵니다.<br>
만약 불러온 정보가 없다면 경고 메세지를 출력하도록 하고 ClubMember를 UserDetails 타입으로 처리하기 위해 ClubAuthMemberDTO로 변환합니다.<br>
또한 ClubMemberRole의 경우 스프링 시큐리티에서 사용하는 SimpleGrantedAuthority로 변환하는데 이 때 'ROLE_' 라는 접두어를 추가해 사용해야 합니다.<br>

# 15. ClubUserDetailsService - loadUserByUsername() 결과 1
---
<br>

![15](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/15.png)
<br>

loadUserByUsername()을 수정한 뒤 프로젝트를 실행해 로그인창에 실제 데이터베이스에 존재하는 계정을 입력한 뒤 로그인합니다.<br>

# 16. ClubUserDetailsService - loadUserByUsername() 결과 2
---
<br>

![16](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/16.png)
<br>

로그인 결과 정상적으로 로그인되어 'sample/member?continue'로 넘어가진 것을 알 수 있습니다.<br>

# 17. member.html 생성
---
<br>

![17](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/17.png)
<br>

로그인이 처리되었으니 사용자의 정보를 화면이나 컨트롤러에서 출력하도록 합니다.<br>
sec:authorize='hasrole()'을 사용해 해당 역할을 가질 경우에만 보이도록 할 수 있습니다. 또한 set:authorize='isAuthenticated'를 사용해 인가와 관련된 정보를 알아내거나 제어가 가능합니다.<br>
다음으로 Authentication의 principal이라는 변수를 사용하면 ClubAuthMemberDTO의 내용을 사용할 수 있습니다.<br>

# 18. member.html 결과
---
<br>

![18](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/18.png)
<br>

로그인 후 'sample/member'에선 위와 같이 로그인한 사용자의 정보를 확인할 수 있습니다.<br>

# 19. SampleController - exMember() 수정 및 결과
---
<br>

![19](/assets/img/web/spring/2023-05-10-[Spring]_스프링_시큐리티_프로젝트를_위한_JPA_처리/19.png)
<br>

컨트롤러에서 로그인된 사용자의 정보를 확인하기 위해서는 `@AuthenticationPrincipal`을 사용해 처리합니다.<br>
SampleController의 exMember()에서 파라미터로 @AuthenticationPrincipal를 작성한 뒤 ClubAuthMemberDTO타입의 clubAuthMember를 받아와 살펴보면 사용자의 정보를 추출하는 것을 확인할 수 있습니다.<br>


