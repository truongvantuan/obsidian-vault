> Có 2 phướng pháp phổ biến nhất cho triển khai cache hệ thống là cache-aside (lazy loading) và write-through.
> Cache-aside cache được cập nhật sau khi dữ liệu được request.
> Write-through cache được cập nhật ngay tức thì database chính có sự thay đổi.

## Cache-aside (lazy-loading)

Là một trong pattern cache phổ biến nhất. Logic truy xuất dữ liệu cơ bản được tóm lược như sau:
1. Khi ứng dụng cần đọc data từ database, nó đầu tiền kiểm tra xem data cần lấy có trong Cache không.
2. Nếu có data ở cache (a cache hit), data đã cache này được trả về.
3. Nếu không có data ở cache (a cache miss), truy vấn data từ database. Lưu data đã truy vấn từ database vào cache, và trả về data này.

Ưu điểm:
1. Cache chỉ lưu data ứng dụng cần. Giúp tối ưu chi phí về dung lượng cache.
2. Dễ triển khai.
3. Mang lại hiệu quả ngay lập tức.
Nhược điểm:
1. Các request tới data chưa được cache cần thêm thời gian cho tải data từ database, set vào cache.

## Write-Through
#needtocomplete