1. What is the difference between Process and Thread? What is Context Switching?
	1. Thread is subset on process.
	2. Context Switching:
		1. Lưu trạng thái của thread đang chạy, khôi phục trạng thái này cho lần chạy sau.
		2. Thực thi các thread đang chờ.
		3. Thời gian switch giữa các threads ảnh hưởng đến hiệu năng của hệ thống.

2. Java performance
	1. Sử dụng StringBuilder khi làm việc với String.
	2. Tái sử dụng Object khi có thể.
		1. Nếu đối tượng bất biến (immutable object), hoặc có thể reset về trạng thái mặc định nên xem xét tái sử dụng.
	3. Ưu tiên sử dụng Primitive thay vì Wrapper Class
		1. Sử dụng Primitive (int, long, boolean) khi không cần dùng đến các tính năng từ Wrapper Class (Integer, Long, Boolean).
	4. Lựa chọn đúng cấu trúc dữ liệu.
		1. HashMap, HashSet that vì List.
	5. Tránh việc Cast object không cần thiết.
		1. Cast object làm chậm code.
	6. Giảm Synchronization Block
		1. Synchronization có thể làm chậm code.
		2. Chia nhỏ Synchronized Block nhỏ nhất có thể.