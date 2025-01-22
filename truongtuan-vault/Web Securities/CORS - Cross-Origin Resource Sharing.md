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


