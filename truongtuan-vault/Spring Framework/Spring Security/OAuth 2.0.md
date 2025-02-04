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
- Resource Owner là người sở hữu tài nguyên.
- Tài nguyên là Protected Resource.
- 3rd party application muốn truy cập protected resource là Client. Cần phân biệt Client và Resource owner.

### Authorization Server

:LiMessageCircleQuestion: Làm sao Client được Protected Resource cho phép truy cập chính nó?
:LiCheckCircle2: Client cần cho Protected Resource xem access token hợp lệ.
- Hình dung access token như là chìa khó vật lý, chìa khóa có thể mở hộp nơi chưa transaction bên trong.
- Client không quan tâm cách khóa được làm ra và cách nó hoạt động ra sao. Client chỉ cần có nó và có thể mở được hộp.
:LiQuestionMarkGlyph: Client lấy access token từ đâu?
:LiCheckCircle2: Token được cấp phát bởi Authorization Server, là một Auth Server mà các bên trong hệ thống tin tưởng.
- Công việc chính của Authorization Server là giữ và cấp phát access token.
- Thực thế Protected Resouces và Auth Server được cung cấp bởi Bank có thể khác server, nếu chung server thì khác endpoint.
:LiQuestionMarkGlyph: Có phải bất kỳ Client nào cũng có thể truy cập Auth Server và lấy Access Token?
:LiCheckCircle2: Chỉ khi Resource Owner đăng nhập vào Auth Server và cho phép Client.

### Cách OAuth 2 hoạt động

![[Pasted image 20250204103309.png]]

**Phase 1: Getting Authorization Code**
1. Resource Owner đăng nhập thành công Authorization Server và cho phép Client truy cập Protected Resource.
2. Authorization Server sinh Authorization Code gửi tới Client thông qua call back api.
**Phase 2: Getting Access Token**
3. Client đăng ký với Authorization Server bằng Authorization Code và Client Credential.
4. Client nhận về credential từ Authorization Server là Client ID và Client Secret.
5. Client sử dụng Client ID và Client Secret để lấy Access Token.
**Phase 3: Using Access Token**
6. Protected Resource xác minh Acess Token từ client cho các lần truy cập tiếp theo.

