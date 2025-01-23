## Origin

- Tính Origin của resource được xác định bởi:
	- `schema` (protocol: http, https).
	- `hostname` (domain).
	- `port`.
- Các resources được gọi là same-origin khi tất cả `schema`, `hostname`, `port` giống nhau.

Same:
- `http://example.com/app1/index.html`
- `http://example.com/app2/index.html`
Not same:
- `http://excample.com/app1`
- `https://example.com/app2`
## Same-Origin policy

![[Pasted image 20250123101944.png]]

- Là một cơ chế bảo mật quan trọng nhằm hạn chế việc một tài nguyên từ một origin có thể tương tác với tài nguyên của origin khác. Trừ khi được sự cho phép rõ ràng và cụ thể (CORS).
- Giúp cách ly các tài nguyên tiềm ẩn nguy hiểm.
- SOP đảm bảo một website chỉ có thể tương tác với resources (API, cookie, DOM, script) cùng chung origin (same origin).

Example:
Một website thực thi JS script (resource A) trên trình duyệt để đọc tài nguyên (resource B) tại một website khác (website đã được user đăng nhập).
- A và B khác Origin, vi phạm Same-Origin policy.

Same-Origin Policy bảo vệ các tài nguyên nào?
1.  DOM access: Client-Side script đang chạy trên một website không thể truy cập và chỉnh sửa DOM của một website khác trừ khi same-origin.
2. Cookies: Cookies từ một origin không thể truy cập bởi script từ một origin khác.
3. Fetch AP: AJAX request thực hiện bởi origin khác bị chặn, trừ khi được chỉ định cụ thể bởi CORS.
4. iframe: Nội dung được tải trong thẻ `<iframe>` từ một origin khác được cô lập.
5. Web storage: Data được lưu trong localStorage, sessionStorage là duy nhất cho các origin  không thể truy cập chéo giữa các origin.

## Cross-Origin Resource Sharing

> Là cơ chế dựa vào HTTP-Header được triển khai bởi Web Browser, cho phép server chỉ định origin nào khác tương tác với resource của server.
> Được xem như là mở rộng của Same-Origin Policy.
### Preflight request

- Browser gửi một "preflight" request tới server nơi lưu giữ cross-origin resource, nhằm kiểm tra trước việc server sẽ có phép thực hiện request thật.
- "Preflight" request như việc hỏi trước server khả năng thực hiện cross-origin request.

:LiMessageCircleQuestion: Khi nào cần thực hiện "preflight" request?
1. Sử dụng các Request method khác GET, POST như: DELETE, PUT, PATCH.
2. Request bao gồm custom headers như: Authorization, Content-Type: application/json, X-Custom-Header.

:LiMessageCircleQuestion: Cách Preflight request hoạt động.
1. Là một OPTIONS request, bao gồm các headers sau:
	- Origin: origin domain thực hiện request.
	- Access-Control-Request-Method: actual request method.
	- Access-Control-Request-Headers: các headers bao gồm lúc gửi actual request.
2. Preflight request được gửi tự động bởi web browser nếu có một trong số các điều kiện nêu trên.
3. Server trả về kết quả cho Preflight request, cụ thể response headers như sau:
	- Access-Control-Allow-Origin: cụ thể origin domain được phép.
	- Access-Control-Allow-Methods: cụ thể request method được phép.
	- Access-Control-Alllow-Headers: cụ thể header được phép.

:LiMessageCircleQuestion: Implement CORS by spring boot?
1. Global CORS configuration.
```java
@Bean  
public WebMvcConfigurer corsConfigurer() {  
    return new WebMvcConfigurer() {  
        @Override  
        public void addCorsMappings(CorsRegistry registry) {  
            registry.addMapping("/**") // Apply to all endpoints  
                .allowedOrigins("https://frontend.app.com") // Allow this origin  
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS") // HTTP methods allowed  
                .allowedHeaders("Authorization", "Content-Type") // Request headers that clients can send  
                .allowCredentials(true) // Allow credentials (cookies)  
                .maxAge(3600); // Cache the preflight response for 1 hour  
        }  
    };  
}
```
2. Specific CORS for controller/enpoint.
```java
@CrossOrigin(  
    origins = "https://frontend.app.com",   
    allowedHeaders = {"Authorization", "Content-Type"},   
    methods = {RequestMethod.GET, RequestMethod.POST}  
)  
@GetMapping("/data")  
public String getData() {  
    return "Hello from the server!";  
}
```