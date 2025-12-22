# 프로시저란 무엇인가?
- 프로시저는 특정 sql 문에 대해 여러 번 입력해야 할 때 이것을 마치 함수처럼 작성해두고 매크로처럼 사용할 수 있게 하는 것이다.

# 프로시저 관련 명령어
1. 프로시저 목록 확인하기<br/>
    ```sql
        show procedure status where db = 'db 이름';
    ```
    <br/>

2. 프로시저 내용 확인하기<br/>
    ```sql
        show create procedure '프로시저 이름';
    ```
    <br/>

3. 프로시저 생성하기<br/>
    ```sql
        mysql> delimiter //
        mysql> create procedure 프로시저이름()
            -> begin
            -> '내가 원하는 sql 문 작성'
            -> end //
        mysql> delimiter ;
    ```
    <br/>

4. 프로시저 호출하기<br/>
    ```sql
        call 프로시저이름();
    ```
    <br/>

<h3>자주 사용할 것 같은 특정 sql 문은 프로시저로 등록해서 사용하는 것도 좋다.</h3>