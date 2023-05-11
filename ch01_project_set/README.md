# 1. 프로젝트 환경설정
- 프로젝트 생성
- 라이브러리 살펴보기
- View 환경설정
- 빌드하고 실행하기
## 1. 프로젝트 설정
- Java 11
- Intellij
- Project
> Project Metadata: hello.spring  
Dependencies: Spring Web, Thymeleaf

## 2. 라이브러리 살폅보기
- spring-boot-starter-web
> spring-boot-starter-tomcat  
spring-webmvc
- spring-boot-starter-thymeleaf
- spring-boot-starter (공통)
> spring-boot > spring-core  
spring-boot-starter-logging: logging, slf4j
### 테스트 라이브러리
- junit, mockito, assertj, spring-test

## 3. View 환경설정
### Welcome Page 만들기
- 스프링 부트가 제공하는 Welcome Page 기능
> static/index.html  
https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-bootfeatures.html#boot-features-spring-mvc-welcome-page
#### thymeleaf 템플릿 엔진
- thymeleaf 공식 사이트: https://www.thymeleaf.org/
- 스프링 공식 튜토리얼: https://spring.io/guides/gs/serving-web-content/
- 스프링부트 메뉴얼: https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-template-engines
```
@Controller
public class HelloController {
    @GetMapping("hello")
    public String hello(Model model) {
        model.addAttribute("data", "hello!!");
        return "hello";
    }
}

```
> `Model`, model.addAttribute("key", "data")

- resources/templates/hello.html
```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
</body>
</html>
```
> `html xmlns:th="http://www.thymeleaf.org"`, ${data} 

## 4. 빌드하고 실행하기
1. ./gradlew build
2. cd buld/libs
3. java -jar hello-spring-0.0.1-SNAPSHOT.jar
4. 실행 확인