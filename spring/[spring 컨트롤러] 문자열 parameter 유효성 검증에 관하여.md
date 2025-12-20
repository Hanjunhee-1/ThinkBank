# 문자열 parameter 유효성 검증이란 무엇인가?
- `localhost:8080/users?userId=a1234`
- DB 에는 사용자의 고유 아이디 즉, Primary Key 를 문자열로 저장하고 있다고 가정하고 위와 같은 URL 에 접근한다고 하자.
- 이 때 해당 URL 에 접근할 수 있게 도와주는 컨트롤러의 함수는 아래와 같을 것이다. <br/>
    ```Java
        @RestController
        @RequestMapping("/users")
        public class UsersController {
            @GetMapping("")
            public String ex1(@RequestParam("userId") String userId) {
                return userId;
            }
        }
    ```
    <br/>
- 지금 예시에서는 userId 의 값을 그대로 반환해주고 있지만 service 측으로 넘겨서 어떤 로직을 수행해야 한다면 해당 값이 정상적인지 유효성 검증을 해주어야 한다. 
    - 만약에 사용자가 빈 문자열을 넘겨주었을 때 에러가 날 수 있기 때문에 `isBlank()` 함수로 비어있는지 확인해주는 것이 좋다.
    - 이외에도 올바르지 않은 형식의 문자열이 존재하는지 확인하기 위한 정규표현식 등을 활용해야 할 수 있다.

- 즉, 핵심 요점은 Spring 에서는 빈 문자열도 받아주기 때문에 해당 부분에 대한 유효성 검증을 해주는 것이 좋다는 것이다.