Transaction là chuỗi các hành động được thực hiện như là một đơn vị 
## Key concepts

1. Atomicity: tất cả các thao tác thành công hoặc không có thao tác nào tạo thay đổi lên resource.
2. Consistency: Database trước và sau transaction đảm bảo tính nhất quán.
3. Isolation: một transaction diễn ra độc lập, các transaction không ảnh hưởng lẫn nhau.
4. Durability: tính bền bỉ, data sau khi được commit cần được lưu lại trạng thái.

## Sử dụng @Transactional

1. Dùng lên class hoặc method.
	1. Class: tất cả các public method được app dụng transactional.
	2. Chỉ lên method: transactional lên method được đánh.
	3. Lên Class và Method: cấu hình @Transactional tại method sẽ ghi đè lên cấu hình tại class.
2. Rollback và exception handling.
	1. Mặc định mọi unchecked exception sẽ được spring rollback. Checked exception cần được bắt thử công qua cấu hình rollbackFor = CheckedException.class
3. Propagation - Nested Transaction
	1. @Transactional cung cấp attribute giúp cấu hình việc Transaction được quản lý như thế nào khi một Transaction Method được gọi trong một Transaction Method khác.
	2. REQUIRED: mặc định, join vào transaction có sẵn, nếu không có tạo mới.
	3. REQUIRES_NEW: tạm dừng transaction hiện tại và tạo mới.
	4. NESTED: thực thi như là một nested transaction nếu database hỗ trợ.
	5. SUPPORTS: sử dụng transaction hiện tại nếu có, nếu không có tì non-transactional.
	6. NOT_SUPPORTED: không transactional.
	7. NEVER: throws exception nếu tồn tại transaction.
	8. MANDATORY: cần một transaction sẵn có.
## Isolation Level

> Isolation level (mức độ cô lập) mô tả cách một transaction tương tác với transaction đống thời khác như nào.
> Cụ thể về khả năng hiển thị (visible) và sửa đổi (modification) dữ liệu chung.