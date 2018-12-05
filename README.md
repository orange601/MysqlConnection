# MysqlConnection
Mysql 연동시 주의사항

Exception
1. com.mysql.cj.exceptions.InvalidConnectionAttributeException
- The server time zone value ~~~ 어쩌구 저꺼구 
- The server time zone value ‘KST’ is unrecognized or represents more than one time zone : mysql-connector-java 버전 5.1.X 이후 버전부터 KST 타임존을 인식하지 못하는 이슈

Solution
1. config.xml 에서 url에 serverTimezone 추가

jdbc:mysql://ip:port/TestDB?characterEncoding=UTF-8&serverTimezone=UTC

나같은 경우는 properties 파일에 저장했으니까
jdbc.url=jdbc:mysql://127.0.0.1:3306/DBName?characterEncoding=UTF-8&serverTimezone=UTC

The reference to entity “serverTimezone” must end with the ‘;’ delimiter.  에러가 발생할 경우 & 대신에 &amp;  사용

jdbc:mysql://ip:port/TestDB?characterEncoding=UTF-8&amp;serverTimezone=UTC


https://yenaworldblog.wordpress.com/2018/01/24/java-mysql-%EC%97%B0%EB%8F%99%EC%8B%9C-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%97%90%EB%9F%AC-%EB%AA%A8%EC%9D%8C/
