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

> Là cơ chế dựa vào HTTP-Header, cho phép server chỉ định origin nào khác tương tác với resource của server.
### Preflight request

- Browser gửi một "preflight" request tới server nơi lưu giữ cross-origin resource, nhằm kiểm tra trước việc server sẽ có phép thực hiện request thật.
- "Preflight" request như việc hỏi trước server khả năng thực hiện cross-origin request.
:LiMessageCircleQuestion: Khi nào cần thực hiện "preflight" request?
1. Sử dụng các Request method khác GET, POST như: DELETE, PUT, PATCH.
2. Request bao gồm custom headers như: Authorization, Content-Type: application/json, X-Custom-Header.
:LiMessageCircleQuestion: Cách Preflight request hoạt động.
1. Là một OPTIONS request, bao gồm các headers sau:
	- Origin: origin domain thực hiện request.
	- 

