# 5. 회원 관리 예제 - 웹 MVC 개발
- 회원 웹 기능 - 홈 화면 추가
- 회원 웹 기능 - 등록
- 회원 웹 기능 - 조회
## 1. 회원 웹 기능 - 홈 화면 추가
### 홈 컨트롤러, 회원 관리용 홈 추가("/")

## 2. 회원 웹 기능 - 등록
### 회원 등록 폼 개발("/members/new"), 회원 등록 폼 HTML
### 회원 등록 컨트롤러
```
@PostMapping("/members/new")
public String create(MemberForm form) {
    Member member = new Member;
    member.setName(form.getName());

    memberService.join(member);

    return "redirect:/";
}
```

## 3. 회원 웹 기능 - 조회
### 회원 컨트롤러 - 조회("/members"), 회원 리스트 HTML
```
<tr th:each="member : ${members}>
    <td th:text="${member.id}"></td>
    <td th:text="${member.name}"></td>
</tr>
```