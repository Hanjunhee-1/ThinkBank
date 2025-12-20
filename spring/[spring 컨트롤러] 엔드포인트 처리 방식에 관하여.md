# Spring 에서의 엔드포인트 처리 방식은 무엇인가?
- 이 모든 일은 NestJS 에 익숙해져있던 나의 안일함 때문이다.
- NestJS 에서는 `localhost:8080/users` 로 `GET` 요청을 보낸다고 했을 때 `localhost:8080/users` 와 `localhost:8080/users/` 모두 동일하게 작동이 되었다.
- 하지만 Spring 에서는 `Mapping` 에 명시한 대로만 작동을 하게 된다.
- 예시는 다음과 같다.<br/>
    ```Java
        @RestController
        @RequestMappring("/users")
        public class UsersController {
            @GetMapping("")
            public String ex1() {
                return "localhost:8080/users";
            }

            @GetMappring("/")
            public String ex2() {
                return "localhost:8080/users/";
            }
        }
    ```
    <br/>
- 만약에 프론트엔드를 개발할 때 헷갈린다면 다음과 같이 명시해주면 된다.
    - `@GetMappring({"", "/"})`