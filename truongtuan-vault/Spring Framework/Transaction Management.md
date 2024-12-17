Transaction là chuỗi các hành động được thực hiện như là một đơn vị.
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

1. Các vấn đề được giải quyết bởi Isolation Level
	1. Dirty Read
		Một transaction đọc uncommitted change bởi một transaction khác. Nếu uncommitted transaction roll back, data đọc bởi transaction này sẽ không còn tồn tại hoặc không toàn vẹn (inconsistent).
		Example:
		- Transaction A cập nhật một bản ghi và không commit.
		- Transaction B đọc bản ghi chưa được commit này.
		- Nếu transaction A roll back, Transaction B đang đọc một bản ghi không hợp lệ.
	2. Non-Repeatable Read
		Một Transaction đọc một bản ghi 2 lần trong thời gian thực thi của nó và nhận về các giá trị khác nhau vì một transaction khác đã thay đổi và commit lên bản ghi đó.
		Example:
		- Transaction A đọc 1 record R.
		- Transaction B cập nhật và commit bản ghi R.
		- Transaction A đọc lại R và nhận được giá trị khác.
	3. Phantom Read
		Một transaction truy vấn database 2 lần với cùng một điều kiện truy vấn (query condition), nhưng kết quả thay đổi bởi vì có transaction khác thay đổi các bản ghi thỏa mãn điều kiện.
		Example:
		- Transaction A truy vấn bản ghi với điều kiện age > 30
		- Transaction B chèn vào một bản ghi có age = 40
		- Transaction A tiếp tục câu truy vấn trên và thấy có 1 bản ghi mới so với kết quả trước đó.
2. Isolation Level
	 Spring cho phép cấu hình isolation level cho transaction thông qua attribute isolation=Isolation.LEVEL
	
	 1. READ_UNCOMMITTED: Cấp độ thấp nhất. Transaction có thể đọc thay đổi của một transaction khác khi chưa được commit.
		 - Issues prevent: None
		 - Problem allowed:
			 - Dirty read
			 - Non-Repeatable read
			 - Phantom read
		- Use case:
			- Thích hợp cho ứng dụng ưu tiên hiệu năng.
			- Ứng dụng cho phép tính không toàn vẹn dữ liệu.
	2. READ_COMMITTED: Transaction không được đọc thay đổi chưa được commit từ transaction khác. Data được commit và nhất quán tại thời điểm đọc, nhưng transaction khác có thể vẫn cập nhật data lúc runtime.
		- Issues prevented: Dirty read
		- Problems allowed:
			- Non-Repeatable Read
			- Phantom Read
		- Use case:
			- Được sử dụng mặc định ở MySQL, PostgreSQL.
			- Thích hợp cho hầu hết mọi ứng dụng chung chung.
	3. REPEATABLE_READ: đảm bảo một transaction đọc bản ghi nhiều hơn một lần, giá trị vẫn nhất quán giữa các lần, kể quả transaction khác chỉnh sửa và commit data này giữa các lần đọc. Level này tạo nhiều consistent snapshot của data.
		- Issues prevented:
			- Dirty Read
			- Non-Repeatable Read
		- Problem allowed:
			- Phantom Read
		- Use case:
			- Ứng dụng tài chính, báo cáo yêu cầu giá trị của một record là nhất quán trong suốt transaction.
	4. SERIALIZABLE: Cấp độ cao nhất. Tất cả transaction được thực thi tuần tự, cô lập hoàn toàn. Clock bất kể truy cập đồng thời nào lên dữ liệu chung.
		- Issues prevented:
			- Dirty Read
			- Non-Repeatable Read
			- Phantom Read
		- Problem allowed:
			- None
		- Use case:
			- Ứng dụng ngân hàng, kho bãi, nhà cung ứng. Bắt buộc tính nhất quán toàn diện.