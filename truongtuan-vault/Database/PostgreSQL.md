
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
	3.     