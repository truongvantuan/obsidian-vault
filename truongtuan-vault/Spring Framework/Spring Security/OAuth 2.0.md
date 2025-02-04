## Giới thiệu

- OAuth 2.0 là một mô hình phân quyền (Authorization Framework), cho phép Client truy cập tài nguyên được bảo vệ thông qua Authorization Server.

## Thành phần cơ bản

**Bài toán thực tế:**
- Bank account cần cho phép ứng dụng bên thứ 3 (third-party application) truy cập thông tin.
- Ứng dụng bên thứ 3 này có thể xem là consumer app, cần try cập các giao dịch cho việc tổng hợp báo cáo chi tiêu hằng tháng.
**Vấn đề gặp phải:**
- Không muốn 3rd party app xem được usernam/password của bank account?
- Chỉ cho phép giới hạn các theo tác, cụ thể xem transaction và không thể tại transaction?
- Khả năng thu hồi (revoke) quyền truy cập bất cứ lúc nào.

### Resources, Owner và Clients

:LiMessageCircleQuestion: Làm sao resource owner (you) cho phép client (3rd party application) truy cập có giới hạn (read, write hoặc cả 2) tới tài nguyên (protected resource)?
- Resource Owner: là người sở hữu tài ng 