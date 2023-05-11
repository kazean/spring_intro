# 4. 스프링 빈과 의존관계
- 컴포넌트 스캔과 자동 의존관계 설정
- 자바 코드로 직접 스프링 빈 등록하기
## 1. 컴포넌트 스캔과 자동 의존관계 설정
회원 컨트롤러가 회원 서비스와 회원 리포지토리를 사용할 수 있게 의존관계를 등록하자
- MemberController, MemberService, MemberRepsotory
> @Autowired  
DI(Dependecy Inject) 의존성 주입: 객체 의존관계를 외부에서 넣어주는 것
### 스프링 빈을 등록하는 2가지 방법
- 컴포넌트 스캔과 자동 의존관계 설정
- 자바 코드로 직접 스프링 빈 등록하기
### 컴포넌트 스캔 원리
- @Component 애노테이션이 있으면 스프링 빈으로 자동 등록
- @Controller 스프링 빈으로 자동 등록 된다
> 컴포넌트 스캔 때문
- @Component 포함 애노테이션: @Controller, @Service, @Repository
- cf: 스프링 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록된다

## 2. 자바코드로 직접 스프링 빈 등록하기
```
@Configuration
public class SpringConfig {
    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
> @Configuration, @Bean
- cf: DI에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 있지만 생성자 주입 권장