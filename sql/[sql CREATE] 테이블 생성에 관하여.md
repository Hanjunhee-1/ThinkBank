# 테이블이란 무엇인가?
- 인간의 관점에서 2차원으로 보이는 데이터의 집합이라고 볼 수 있다.
- column 에는 필드(속성) 들이 열거되어있다.
- row 에는 column 에 존재하는 모든 속성들을 하나씩 가지고 있다. 즉, row 가 완전한 데이터라고 볼 수 있고 column 은 부분 데이터라고 볼 수 있다.
<br/>

# 테이블 생성은 어떻게 하는가?
- 테이블 생성 명령어인 `create table [테이블 이름] (...);` 을 통해 생성한다.
- 아래는 테이블 생성에 대한 예시이다. <br/>
    ```SQL
        create table users (
            signature varchar(36) primary key default (uuid()),
            id varchar(20) unique not null,
            password varchar(60) not null,
            nickname varchar(20) unique not null,
            createdAt timestamp default current_timestamp,
            role enum('USER', 'ADMIN') not null default 'USER'
        );

        create table diaries (
            id int auto_increment primary key,
            title varchar(255) not null,
            contents text not null,
            craetedAt timestamp default current_timestamp,
            isPublished enum('PRIVATE', 'PUBLIC') not null default 'PRIVATE',
            user_signature varchar(36) not null,
            constraint fk_diaries_users
            foreign key (user_signature)
            references users (signature)
            on delete cascade
            on update cascade
        );

        create table logs (
            id int auto_increment primary key,
            date timestamp not null,
            count int default 0,
            user_signature varchar(36) not null,
            constraint fk_logs_users
            foreign key (user_signature)
            references users (signature)
            on delete cascade
            on update cascade
        );
    ```
    <br/>

    - `varchar(n)`: n 길이 만큼의 문자열을 저장한다.
    - `primary key`: 해당 테이블의 기본키이자 각 row 가 서로 다른 값을 가져야 하는 고유 값이 된다.
    - `default`: 테이블에 값이 입력될 때 기본으로 입력되는 값을 의미한다.
    - `uuid()`: uuid 를 만들어서 넣어준다.
    - `unique`: 각 row 마다 서로 다른 값을 가져야 한다.
    - `not null`: 절대 null 값이 입력되는 것을 허용하지 않는다.
    - `timestamp`: 시간을 `YYYY-MM-DD HH:MM:SS` 형식으로 입력해준다.
    - `current_timestamp`: 현재 시간을 `YYYY-MM-DD HH:MM:SS` 형식으로 입력해준다.
    - `enum()`: varchar, int 는 타입을 제한한다면 enum 은 해당 필드에 입력될 수 있는 입력값 자체를 제한한다.
    - `int`: 숫자형으로 값이 저장된다.
    - `auto_increment`: 값이 숫자형일 경우 primary key 를 굳이 넣어주지 않아도 알아서 값이 1씩 증가하여 입력되게 한다. 해당 값을 조회하고 싶다면 `show table status where name = [테이블 이름]` 을 입력하여 확인한다.
    - `text`: varchar(n) 보다 더 큰 값을 넣을 수 있다.
    - `constraint`: 외래키 설정 시 제약 조건 이름 정도로 기억해두자.  
    - `foreign key`: 외래키로 설정할 필드를 명시한다. 
    - `references [테이블 이름] [해당 테이블의 primary key 필드명]`: 외래키를 설정할 필드가 참조할 값을 의미한다.
    - `on delete cascade`: 외래키가 참조하는 값이 삭제될 경우 해당 row 도 삭제된다.
    - `on update cascade`: 외래키가 참조하는 값이 변경될 경우 해당 row 도 변경된다.