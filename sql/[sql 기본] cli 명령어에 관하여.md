# MySQL 8.0 command line client 명령어
- `show databases`: 현재 내 서버에 존재하는 모든 데이터베이스를 조회한다.
- `create database [db 이름]`: 새로운 데이터베이스를 생성한다.
- `drop database [db 이름]`: 데이터베이스를 삭제한다. -> 안에 존재하는 테이블 정보도 모두 삭제된다.
- `use database [db 이름]`: 사용하고자 하는 데이터베이스에 접근한다. 테이블을 생성하고 싶으면 테이블을 생성하고 싶은 데이터베이스에 당연히 접속이 되어있어야 한다.
- `system cls`: CLI 로 계속 작업하다보면 history 가 더럽게 많이 남는다. 그럴 때 이 명령어를 입력하면 입력창을 깨끗하게 해준다.