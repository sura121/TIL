## SPRING security 인증 절차


![](http://cfile5.uf.tistory.com/image/231EC041553760DE21DBBA)

위의 그림에서 크레덴셜은 비밀번호를 의미한다.

1. 인증요청에 해당하는 URL을 감지하면,

 - 최초로 AbstractAuthenticationProcessingFilter를 구현한 클래스가 요청을 가로 챈다.
 - 보통 JAVA CONFIG에서는 protected void configure(HttpSecurity http) throws Exception 메소를 오버라이드 하여 http 전반적인 보안정책을 설정한다 하지만 http.formLogin()을 이용하면 기본적으로 AbstractAuthenticationProcessiongFilter를 구현한 UsernamePasswordAuthenticationFilter를 이용하게 된다.

*UsernamePasswordAuthenticationFilter 에서는 인증(로그인) 요청에 대해서 기본적으로 GET PARAMETER로 인증 정보가 들어오는 것을 허용하지 않고 있다. Http Method를 POST만 지원하도록 되어있다.*

*REQUEST로 들어온 USERNAME과 PASSWORD에 해당하는 파라미터의 정보를 UsernamePasswordAuthenticationToken 에 담는다. 이 토큰은 그냥 사용자명과 비밀번호를 담는 단순 도메인객체이다.*

*UsernamePasswordAuthenticationFilter가 주입 받은 AuthenticationManager의 authenticat 메소드를 호추한다. 이때, 인자로 UsernamePasswordAuthenticationToken를 준다.*

_AuthenticationManager는 인터페이스 이며 이 인터페이스를 구현한 ProviderManager를 기본으로 사용한다._

*AuthenticationManager는 사용자명/비밀번호를 실질적으로 인증한다.*

*auth를 이용하여 AuthenticationManager를 설정하면 된다. AuthenticationManager는 AuthenticationManager에 연결된 Provider를 이용하여 인증 작업을 진행 한다. 보통 데이터베이스에 저장된 사용자 정보로 인증을 많이한다. 이때 auth.UserDetaulsService(userDetailsService)를 이용하면, 자동으로 AuthenticationManager에 DaoAuthenticationProvider가 연결된다. 이 때 DaoAuthenticationProvider를 설정할 때, 위에서 적혀있듯이 인자로 userDetaulsService를 받는다. UserDetaulsService로 username을 이용하여 사용자 정보를 디비에서 조회하고 UserDetails 객체를 리턴한다. *

*DaoAuthenticationProvider 는 protected void additionalAuthenticationChecks(UserDetails userDetails, UsernamePasswordAuthenticationToken authentication)throws AuthenticationException
위 메소드를 이용하여 검증을 진행하는데 위 메소드는 ProviderManager 의 authenticate 메소드 내부에서 Provider 의 authenticate를 호출해주고 DaoAuthenticationProvider의 상위 클래스인 AbstractUserDetailsAuthenticationProvider에서 additionalAuthenticationChecks 를 호출한다.아무튼, additionalAuthenticationChecks메소드는 UserDetails와 UsernamePasswordAuthenticationToken을 인자로 받는데, UserDetails 는 UserDetailsService 에서 디비 조회후, 결과값이고, UsernamePasswordAuthenticationToken 은 로그인 폼에서 넘긴 사용자가 입력한 유저 아이디와 비밀번호이다. additionalAuthenticationChecks 메소드 내부에서 UserDetails 내용과 UsernamePasswordAuthenticationToken 의 내용을 비교하고, 값이 동일하다면 인증 성공이다.*
