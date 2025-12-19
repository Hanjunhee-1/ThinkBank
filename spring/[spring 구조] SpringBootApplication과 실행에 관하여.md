# SpringBootApplication 이 무엇인가?
- SpringBoot 프로젝트를 실행하기 위한 것이다. 
- `@SpringBootApplication` 이라는 어노테이션을 class 위에 명시하여 사용한다.
- 생긴 것은 다음과 같이 생겼다.
    ![img](./img/[spring%20구조]SpringBootApplication에%20관하여(1).png)
    그냥 Java 파일을 쌩(?)으로 만들었을 때의 모습에서 SpringBoot 어노테이션이 붙은 모습이다.
<br/><br/><br/>

# SpringBootApplication 에서 실행은 어떻게 하는가?
- 해당 파일에서 우클릭을 하고 `Run as > Spring Boot` 를 누르면 된다.
<br/><br/><br/>

# 주의사항이 따로 있는가?
- 실행을 시켜야하는 controller, service 등이 포함된 폴더 또는 파일은 SpringBootApplication 어노테이션이 명시된 파일과 동일한 계층에 존재하거나 그 하위에 존재해야 한다.
- `NestJS` 에서는 폴더 구조를 main 이 실행되는 곳과 다른 곳에 두는 식으로 진행했어서 spring 에서도 그렇게 했다가 기껏 만들어놓았던 api 가 실행이 안되어 상당히 애를 먹었었다. 아래와 같이 두면 된다.
    ![img](./img/[spring%20구조]SpringBootApplication에%20관하여(2).png)
