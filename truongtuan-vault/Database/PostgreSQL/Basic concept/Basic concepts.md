
## Multi-Version Concurrency Control (MVCC)

> PostgreSQL cung cấp nhiều công cụ giúp quán lý truy cập database đồng thời (concurrency).
> Mỗi câu lệnh SQL sẽ thấy snapshot của data (database version) tại một thời điểm cụ thể (a specific point in time), bất kể trạng thái hiện tại của data.
> Snapshot data này được tại trong khi thực thi truy vấn hoặc transaction.

1. Consistency
	1. Một snapshot tương ứng với một bản sao data, phản ánh trạng thái của data tại lúc query/transaction bắt đầu. Các thay đổi lên data bởi transaction khác sau thời điểm tạo snapshot sẽ được bỏ qua.
	2. Nó dảm bảo rằng transaction hiện tại sẽ không thấy thay đổi imcomplete/uncommited của transaction khác.
2. Snapshot
	1. PostgreSQL sử dụng MVCC để quản lý các transaction đồng thời.
	2. Khi transaction bắt đầu, một snapshot được tạo để theo dõi các records trong phạm vị ảnh hưởng của trasaction (transaction nhìn thấy).
	3. Các snapshot xác định database rows có thể nhìn thấy dựa trên **Transaction ID** của chúng.
3. Transaction isolation levels
	1. Hành vi của Snapshot dựa trên cấp độ cô lập transaction (isolation level).
	2. READ COMMITED: Data được snapshot tại thời điểm bắt đầu của query, query chỉ thấy thay đổi đã được commit tại thời điểm này.
	3. REPEATABLE READ or SERIALIZABLE: Data được snapshot tại thời điểm bắt đầu transaction, query thấy trạng thái của data như nó tồn tại tại thời điểm snapshot.
4. How snapshot work?
	1. Một snapshot chứa metadata sau:
		1. Transaction ID hiện tại.
		2. Danh sách active transaction (transaction chưa được commit kể từ thời điểm lấy snapshot).
		3. Transaction sau thời điểm snapshot sẽ bỏ qua (ignored).
	2. Việc sử dụng metadata trên sẽ xác định records được nhìn thấy bởi transaction.
5. Ứng dụng của snapshot
	1. Tính nhất quán tại một thời điểm: đảm bảo tính nhất quán trong việc đọc dữ liệu của các câu query có thời gian chạy lâu hoặc các job báo cáo. Nghĩa là không có sự thay đổi data trong quá trình câu query chạy.
	2. Indexing và Vacuuming: cho phép PostgreSQL xác định các phiên bản record cũ, không còn được nhìn thấy bởi transaction và sẽ được loại bỏ vởi Vacuuming.
	3. Concurrency: cho phép đồng thời truy cập data mà không block lẫn nhau.

## Transaction

> Transaction là chuỗi một hoặc nhiều hành động (step) được thực thi như là một đơn vị công việc (logical unit of work).

- Các trạng thái trung gian giữa các bước không thể nhìn thấy bởi transaction đồng thời khác.
- Nếu có lỗi xẩy, không có bước nào trong transaction tác động đến data.
- Khi các transaction diễn ra đồng thời, không nhìn thấy trạng thái chưa hoàn thành giữa các transaction với nhau.

## Write-Ahead Logging


## Query Processing
![[Pasted image 20250108112637.png]]
1. Parsing
- Parser kiểm tra tính đúng đắn trong câu query về mặt cú pháp.
- Parser phân tích câu truy vấn và đưa ra cấu trúc Tree các thành phần cấu thành câu truy vấn.
2. Rewriter
- Kết quả từ Parser là input cho Rewriter
- Rewriter sẽ viết lại và tối ưu query tree từ Parser.
- Áp dụng các Rule lên câu truy vấn.
- Row-level security sẽ được triển khai ở bước này.
3. Planner
4. Executor

## EXPLAIN

> EXPLAIN dùng để hiển thị kế hoạch thực thi của câu truy vấn.
> EXPLAIN có thể sử dụng lên SELECT, CREATE, UPDATE, DELETE, EXECUTE, DECLARE, CREATE TABLE AS.

**Syntax:**
`EXPLAIN [ (parameter [, ...] ) ] statement`

- ANALYZE
	- Tham số này thực thi câu lệnh và trả về query plan. Kết quả thực thi câu lệnh được loại bỏ nhưng câu lệnh vẫn được thực thi.
	- Kết hợp với `ROLLBACK` để hủy bỏ kết quả của câu lệnh, nếu câu lệnh làm thay đổi trạng thái data.
```postgresql
BEGIN;

EXPLAIN (ANALYZE) INSERT INTO Animal 
(ani_id, name, weight_kg, cat_id, enc_id) 
VALUES (28, 'Robin Robin', 0.5, 1, 2);

ROLLBACK;
```

- VERBOSE
	- Hiển thị thêm thông tin bổ sung.
- COSTS
	- Được áp dụng mặc định trong PostgreSQL.
- FORMAT
	- Xác định kiểu dữ liệu trả về của kết quả EXPLAIN