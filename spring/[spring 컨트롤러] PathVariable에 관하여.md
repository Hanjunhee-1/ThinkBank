# PathVariable 이 무엇인가?
- `localhost:8080/api/users/123`
- 위와 같은 URL 에 접근할 것이다. 여기서 123 은 사용자의 고유 아이디라고 하자.

    이 때 123 은 PathVariable 이 된다. NestJS 의 경우에는 `:parameter` 의 형식으로 받아주었는데 Spring 에서는 `@PathVariable("parameter") String parameter` 형식으로 받아준다.