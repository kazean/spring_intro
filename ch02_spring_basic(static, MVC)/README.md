# 2. 스프링 웹 개발 기초
## 1. 정적 컨텐츠
- 스프링 부트 정적 컨텐츠 기능
- https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-bootfeatures.html#boot-features-spring-mvc-static-content
- resources/static/hello-static.html

## 2. MVC와 템플릿 엔진
- MVC: Model, View, Controller
- Controller
```
@GetMapping("hello-mvc")
public String helloMvc(@RequestParam("name") String name, Model name) {
    model.addAttribute("name", name);
    return "hello-template";
}
```
- View(resources/static/hello-template.html)
- MVC 템플릿 엔진 이미지
> helloController > `viewResolver`

## 3. API
### @ResponseBody 문자 변환
```
@GetMapping("hello-string")
@ReponseBody
public String helloString(@RequestParam("name") String name) {
    return "hello " + name;
}
```
> @Reponsebody를 사용하면 뷰 리졸버를 사용하지 않음
### @ResponseBody 객체 반환
> return hello; //Class
### @ResponseBody 사용 원리
- @ResponseBodt 사용
> HTTP의 body에 문자 내용을 직접 반환  
viewResolve 대신에 `HttpMessageConverter`가 동작  
기본 문자처리: StringHttpMessageConverter  
기본 객체처리: MappingJackson2HttpMessageConverter