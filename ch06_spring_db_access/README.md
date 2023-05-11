# 6. 스프링 DB 접근 기술
## 1. H2 데이터베이스 설치
### 테이블 생성하기 - member
- http://localhost:8082

## 2. 순수 JDBC
### 환결 설정
- build.gradle파일에 jdbc, h2 관련 라이브러리 추가
> spring-boot-starter-jdbc, com.h2database:h2
- 스프링 부트 데이터베이스 연결 설정 추가
```
spring
    datasource
        url: jdbc:h2:tcp://localhost/~/test
        driver-class-name: org.h2.Driver
        username: sa
        password: 
```
### JDBC 리포지토리 구현
- JdbcMemberRepository
```
private final DataSource dataSource;

public save, findById(..) {

    pstmt.executeUpdate();
    pstmt.executeQuery()
}

private Connection getConnection() {
    return DataSourceUtils.getConnection(dataSource)
}

private void close(Connection conn) {
    DataSourceUtils.releaseConnection(conn, dataSource);
}
```
> DataSourceUtils, pstmt.executeUpdate(), pstmt.executeQuery()
### 스프링 설정 변경
- 개방 폐쇄 원칙(OCP, Open-Closed Principle)
> 확장에는 열려있고, 수정, 변경에는 닫혀있다
- 스프링의 DI(Dependencies Injection)을 사용하면 기존 코드를 전혀 손대지 않고, 설정만으로 구현 클래스를 변경할 수 있다

## 3. 스프링 통합 테스트
- MemberServiceIntegrationTest
> @SpringBootTest: 스프링 컨테이너와 테스트를 함께 실행한다  
@Transactional: 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다.

## 4. 스프링 JdbcTemplate
- JdbcTemplate, Mybatis 같은 라이브러리는 JDBC API에서 본 반복 코드 대부분 제거해준다. 하지만 SQL은 직접작성
- JdbcTemplateMemberRepository
> SimpleJdbcInsert
### JdbcTemplate을 사용하도록 스프링 설정 변경 - JDBC와 동일

## 5. JPA
- 기본적인 SQL도 JPA가 만들어서 실행해준다
- 데이터 중심 설계에서 객체 중심의 설계로 패러다임 전환을 할 수 있다.
- 개발 생산선을 크게 높일 수 있다
### build.gradle JPA 관련 라이브러리 추가
- spring-boot-starter-data-jpa
> jdbc 관련 라이브러리를 포함한다, 따라서 jdbc는 제거해도 된다
### 스프링 부트에 JPA 설정 추가
```
spring
    jpa
        show-sql: true // logging으로 전환 org.hibernate.SQL
        hibernate.ddl-auto: create
```
> show-sql, ddl-auto: none/create
### JPA 엔티티 매핑
- Member
> @Entity, @Id, @GeneratedValues(strategy = GenerationType.IDENTITY), Getter, Setter
### JPA 회원 리포지토리
- JpaMemberRepository
```
private fianl EntityManager em;

save, findById, ...() {
    em.persist(member)
    em.find(Member.class, id);
    em.createQuery("select m from Member m where m.name = :name", Member.class)
        .setParameter("name", name)
        .getResultList();
}
```
### 서비스 계층에 트랜잭션 추가
- JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.
### JPA를 사용하도록 스프링 부트 설정 변경
- EntityManager

## 6. 스프링 데이터 JPA
- 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공
### 스프링 데이터 JPA 회원 리포지토리
- <I> SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository
### 스프링 데이터 DataJpa 설정
### 스프링 데이터 JPA 제공 클래스
- Repository < CrudRepository< PagingAndSortingRepository < JpaRepository
- 스프링 데이터 JPA 제공 기능
> 인터페이스를 통한 기본적인 CRUD, 쿼리메소드 기능, 페이징기능 자동 제공