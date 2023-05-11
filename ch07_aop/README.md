# 7. AOP
## 7-1. AOP 가 필요한 상황
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
### MemberService 회원 조회 시간 측정 추가 (AOP 전)
### 문제
- 시간을 축정하는 기능은 핵심 관심 사항이 아니다
- 시간 측정하는 로직은 공통 관심 사항이다
- 유지보수가 어렵다
- 별도의 공통 로직으로 만들기 어렵다

## 7-2. AOP 적용
- AOP: Aspect Oriented Programming
- 공통 관심사항 vs 핵심 관심사항 분리
### 시간 측정 AOP 등록
```
@Component
@Aspect
public class TimeTraceAOP {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint jointPoint) throws Throwable {
        long start = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());

        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;

            System.out.println("END: " + joinPoint.toString() + " " + timeMs + "ms);
        }
    }
}
```
> @Component, @Aspect
### 해결
- 핵심 관심사항과 공통 관심사항을 분리한다
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.
- 변경이 필요하면 이 로직만 변경하면 된다
### 스프링의 AOP 동작 방식 설명
- AOP 적용 전 의존관계
- AOP 적용 후 의존관계
> 프록시