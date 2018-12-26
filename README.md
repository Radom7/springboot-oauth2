# springboot-oauth2
## 主要maven依赖
```
<!-- 注意是starter,自动配置 -->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>
<!-- 不是starter,手动配置 -->
<dependency>
	<groupId>org.springframework.security.oauth</groupId>
	<artifactId>spring-security-oauth2</artifactId>
	<version>2.3.4.RELEASE</version>
</dependency>
<!-- 将token存储在redis中 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

## 访问 
password模式：
```
http://localhost:8080/oauth/token?username=user_1&password=123456&grant_type=password&scope=select&client_id=client_2&client_secret=123456
```
相应：
```
{
    "access_token": "bca4bf04-7cb5-4ef5-a12e-dded7712cd81",
    "token_type": "bearer",
    "refresh_token": "a0f7424a-b8d3-4c60-95c8-6e5fb9ad3226",
    "expires_in": 43199,
    "scope": "select"
}
```
client模式：
```
http://localhost:8080/oauth/token?grant_type=client_credentials&scope=select&client_id=client_1&client_secret=123456
```
相应：
```
{
    "access_token": "4ca2328d-cff9-422f-ae74-cfce87291b4c",
    "token_type": "bearer",
    "expires_in": 43199,
    "scope": "select"
}
```

已对order资源进行限制保护

若不加token对order资源访问：
```
http://localhost:8080/order/1
```
得到的相应：
```
{
    "error": "unauthorized",
    "error_description": "Full authentication is required to access this resource"
}
```

若加token对order资源访问：
```
http://localhost:8080/order/1?access_token=4ca2328d-cff9-422f-ae74-cfce87291b4c
```
得到的相应：
```
order id : 1
```
