# 3. 회원 관리 예제 - 백엔드 개발
- 비지니스 요구사항 정리
- 회원 도메인과 리포지토리 만들기
- 회원 리포지토리 테스트 케이스 작성
- 회원 서비스 개발
- 회원 서비스 테스트
## 1. 비지니스 요구사항 정리
- 데이터: 회원ID, 이름
- 기능: 회원 등록, 조회
- 아직 데이터 저장소가 선정되지 않음
### 일반적인 웹 애플리케이션 계층 구조
- 컨트롤러: 웹 MVC Controller
- 서비스: 핵심 비지니스 로직 구현
- 리포지토리: DB 접근
- 도메인: 비지니스 도메인 객체

## 2. 회원 도메인과 리포지토리 만들기
## 3. 회원 리포지토리 테스트 케이스 작성
자바는 JUnit이라는 프레임워크로 테스트를 실행
- MemoryRepositoryTest
> @AfterEach: 각 테스트가 종료될 때마다 이 기능을 실행한다  
@Test
- 테스트는 각각 독립적으로 실행되어야 한다. 테스트 순서에 의존관계가 있는 것은 좋은 테스트가 아니다.

## 4. 회원 서비스 개발
## 5. 회원 서비스 테스트
회원 서비스 코드를 DI 가능하게 변경
```
public class MemberService {
    private fianl MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
}
```
### 회원 서비스 테스트
- MemberServiceTest
> @BeforeEach, @AfterEach, @Test