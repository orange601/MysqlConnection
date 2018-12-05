# MysqlConnection
Mysql 연동시 주의사항


1. Mysql 연동시 mysql-connector-java 버전 5.1.X 이후 버전 부터 KST 타임존을 인식하지 못하는 경우가 발생한다.

그럴땐 jdbc.url=jdbc:mysql://127.0.0.1:3306/DBName?characterEncoding=UTF-8&serverTimezone=UTC
serverTimeZone을 설정한다

**자세한내용**

- Exception 내용 : com.mysql.cj.exceptions.InvalidConnectionAttributeException

- The server time zone value ~~~ 어쩌구 저꺼구 

( The server time zone value '´ëÇÑ¹Î±¹ Ç¥ÁØ½Ã' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support. )

- The server time zone value ‘KST’ is unrecognized or represents more than one time zone : mysql-connector-java 버전 5.1.X 이후 버전부터 KST 타임존을 인식하지 못하는 이슈


**Solution**
- config.xml 에서 url에 serverTimezone 추가

````xml
jdbc:mysql://ip:port/TestDB?characterEncoding=UTF-8&serverTimezone=UTC
````

나같은 경우는 properties 파일에 저장했으니까

````propeties
jdbc.url=jdbc:mysql://127.0.0.1:3306/DBName?characterEncoding=UTF-8&serverTimezone=UTC
````

만약 The reference to entity “serverTimezone” must end with the ‘;’ delimiter.  에러가 발생할 경우
````xml
 # & 대신에 &amp;  사용

jdbc:mysql://ip:port/TestDB?characterEncoding=UTF-8&amp;serverTimezone=UTC
````

[출처]

https://yenaworldblog.wordpress.com/2018/01/24/java-mysql-%EC%97%B0%EB%8F%99%EC%8B%9C-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%97%90%EB%9F%AC-%EB%AA%A8%EC%9D%8C/
