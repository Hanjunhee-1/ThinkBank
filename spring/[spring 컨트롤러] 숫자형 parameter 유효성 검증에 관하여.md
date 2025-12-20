# 숫자형 parameter 유효성 검증이 무엇인가?
- `localhost:8080/diaries?diaryId=123`
- DB 에는 일기의 고유 아이디 즉, Primary Key 를 정수형으로 저장하고 있다고 가정하고 위와 같은 URL 에 접근한다고 가정하자. 
- 이 때 해당 URL 의 접근을 도와주는 컨트롤러의 함수는 아래와 같을 것이다. <br/>
    ```Java
        @RestController
        @RequestMapping("/diaries")
        public class DiaryController {
            @GetMapping("")
            public int ex1(@RequestParam("diaryId") Integer diaryId) {
                return diaryId;
            }
        }
    ```
    <br/>

- 지금은 diaryId 를 그대로 반환해주고 있지만 service 측으로 넘겨서 어떤 로직을 수행해야 한다면 해당 값이 정상적인지 유효성 검증을 해주어야 한다.
    - 이 때는 그냥 int 가 아닌 Integer 를 사용해야 null 체크에 대해 수월해진다. 
    - null 체크를 하는 이유는 `localhost:8080/diaries?diaryId=` 으로 요청이 가능하기 때문이다.