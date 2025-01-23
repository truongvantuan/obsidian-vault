## Throwable
---

> - Throwable là parent class (top-level class) của tất cả Exception và Error trong Java.
> - Throwable đại diện cho tất cả các  vấn đề có thể phát sinh trong quá trình thực thi một chương trình.
> - Subclass của Throwable là Error và Exception đại diện cho các loại khác nhau của vấn đề.

## Errors
---
> - Đại diện cho các vấn đề không thể cover, handle bởi chương trình.
> - Errors là uncheckable, nằm ngoài phạm vi xử lý, điều khiển của chương trình.
> - Thường liên quan đến JVM.

Đặc điểm:
1. Nằm ngoài phạm vi xử lý của chương trình.
2. Gây dừng ứng dụng hoặc khởi động lại JVM.
3. Không thường được catch hoặc handle.

Example:
1. **OutOfMemoryError**
	- Hết bộ nhớ RAM cho JVM hoạt động, tràn bộ nhớ RAM.
	- Không thể allocate bộ nhớ cho JVM Heap.
	- **Metaspace**
		- Được giới thiệu từ Java 8, giải quyết các vấn đề của PermGen (kích thước bộ nhớ fix cứng, phụ thuộc vào Heap).
		- Fixed Size từ PermGen: không thể linh hoạt thay đổi size lúc runtime. Các framework như Spring, Hibernate với khả năng load class tự động thường gặp lỗi OutOfMemoryError.
		- PermGen trước Java 8 là một phần của Heap, việc phụ thuộc làm khó tối ưu.
		- 
