## OAuth2 support

```java
spring.cloud.openfeign.oauth2.enabled=true
```

- Khi enabled Oauth2 cho Open Feign và ứng dụng được triển khai Oauth2 client thì bean của class `OAuth2AccessTokenInterceptor` sẽ được tạo. 
- Trước mỗi request, interceptor sẽ trích xuất access token và đưa vào Header attribute.
