# Spring 과 MySQL 연동
※ 당연히 PC 에 MySQL 이 설치가 되어있어야 한다.

# 1. build.gradle 파일 수정하기 (dependency 설정)
```
    // JPA 를 사용하기 위함
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

    // MySQL Driver 를 사용하기 위함
    reuntimeOnly 'com.mysql:mysql-connector-j'
```

위와 같은 내용을 `dependencies` 에 추가해준다. Spring 프로젝트를 생성할 때 넣어줬다면 알아서 추가가 되어있을 것이다.

# 2. application.properties 파일 수정하기

```
    # --- MySQL 연결 설정 ---
    spring.datasource.url=jdbc:mysql://localhost:3306/{DB_NAME}?useSSL=false&serverTimezone=Asia/Seoul&characterEncoding=UTF-8
    spring.datasource.username={DB_USER}
    spring.datasource.password={DB_PASSWORD}
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

    # --- JPA 설정 ---
    spring.jpa.hibernate.ddl-auto=none
    spring.jpa.show-sql=true
    spring.jpa.properties.hibernate.format_sql=true
    spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```

`spring.jpa.hibernate.ddl-auto=none`: 이건 update 로 해두면 로컬에서 수정한 값을 DB 에 바로 덮어씌우니 주의해야 한다.

Mysql 과 JPA 에 대한 설정을 진행해준다. username 과 password 는 민감한 정보라서 github 와 같은 public 공간에 프로젝트를 올릴 때는 주의해야하는데 이를 관리하는 방법은 두 가지가 있다.
    
(1) OS 자체의 환경변수 사용하기 -> 이건 set DB_USER = "root" 이런 식으로 하고 application.properties 에서 ${DB_USER} 와 같이 입력하여 활용하는 방식이다.

(2) 프로파일 별로 관리하기
src/main/resources/application.properties 가 존재하는데 프로파일을 추가해주는 것이다.
그냥 application-{PROFILE_NAME}.properties 로 하면 된다. 예를 들면, local 에서는 DB 정보를 보여도 상관이 없으니 application-local.properties 라는 파일을 만들고 그 안에 

```
    spring.datasource.username={DB_USER}
    spring.datasource.password={DB_PASSWORD}
```

이런 예민한 정보를 그냥 넣어두는 것이다. 

# 3. Entity 생성하기
객체를 생성하는 것이다. 객체는 DataBase 에 생성해두거나 이제 생성할 테이블이라고 보면 된다.

```Java
    package com.example.demo.users.domain;

    import jakarta.persistence.Column;
    import jakarta.persistence.Entity;
    import jakarta.persistence.GeneratedValue;
    import jakarta.persistence.GenerationType;
    import jakarta.persistence.Id;
    import jakarta.persistence.Table;
    
    // lombok 이 참 편하다.
    import lombok.Getter;
    import lombok.NoArgsConstructor;
    import lombok.Setter;

    @Getter
    @Setter
    @Entity
    @Table(name = "users")
    @NoArgsConstructor
    public class Users {
        
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        
        @Column(nullable = false, length = 255)
        private String nickname;
        
        @Column(nullable = false, length = 255)
        private String password;
    }
```

위와 같은 식으로 생성해주면 된다.

# 4. Repository 작성하기
Repository 는 JpaRepository 를 사용하기 위해 생성한다. 만약 JpaRepository 를 안 쓴다면 DAO 를 직접 만들고 SQL query 를 직접 일일이 작성해야 하는데 JPA 덕분에 이런 것에서 해방된다.

```Java
    package com.example.demo.users.repository;

    import org.springframework.data.jpa.repository.JpaRepository;

    import com.example.demo.users.domain.Users;

    public interface UsersRepository extends JpaRepository<Users, Long>{
        boolean existsByNickname(String nickname);
    }
```
Repository 는 JpaRepository 를 상속받아서 작성한다. Entity 를 작성할 때 입력한 필드들에 대한 기본적인 쿼리들이 어느 정도 있지만 다른 쿼리가 필요하다면 위와 같이 함수로 작성해줄 수 있다.

# 5. 실제로 사용해보기
`Service` 에서 `Repository` 를 주입하여 DB에 접근하고 `Controller` 에서 `Service` 를 주입하여 사용해보자.