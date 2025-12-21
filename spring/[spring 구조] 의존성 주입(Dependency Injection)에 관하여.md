# 의존성 주입(Dependency Injection) 이란 무엇인가?
- 의존성 주입은 컨트롤러, 서비스, 모듈 등이 각각의 독립된 역할을 할 수 있도록 하기 위해 사용하는 것이다.
- 예를 들어, 컨트롤러는 URL 에 접근하는 것을 주로 하고 서비스는 비즈니스 로직을 처리하는 것을 주로한다. 그런데 만약에 컨트롤러에서 모든 것을 처리하게 한다면 이는 각각 독립된 역할을 하는 것이라고 볼 수 없다.
- 그래서 의존성 주입을 통해 각각의 독립된 역할을 할 수 있도록 하는 것이다. 이렇게 하면 나중에 유지 및 보수도 쉬워진다.

# 의존성 주입 예시
```Java
    @RestController
    @RequestMapping("/users")
    public class UsersController {
        private final UsersService usersService;

        public UsersController(UsersService usersService) {
            this.usersService = usersService;
        }
    }
``` 
<br/>

```Java
    @Service
    public class UsersService {
        // ...
    }
```
<br/>

- 위와 같이 의존성 주입이 이루어지고 컨트롤러에서 서비스의 비즈니스 로직을 사용할 수 있게 된다.
1. `final` 을 명시함으로써 객체가 주입된 이후에 수정될 수 없다는 `불변성` 을 보장할 수 있게 된다.
2. 컨트롤러의 생성자를 통해 서비스의 객체가 있어야만 동작할 수 있다는 것을 명시할 수 있다.
3. 순환참조가 발생했을 경우 스프링 빈에 등록이 되어있기 때문에 스프링 컨테이너에서 바로 알 수 있다. 
    - 만약에 예시 대로 하지 않고 필드 혹은 세터 주입을 통해 의존성 주입이 이루어졌을 경우에는 디버깅이 힘들어진다.