Là câu lệnh SQL dùng để định nghĩa và quản lý cấu trúc của các đối trượng Database như Table, Index, View, Schema.
DDL bao gồm CREATE, ALTER, DROP, TRUNCATE.
## TRUNCATE

- Sử dụng để xóa nhanh toàn bộ records từ một table.
- Làm việc ở cấp độ table.
- Nếu table có auto-increment, TRUNCATE reset về giá trị ban đầu.
- Trigger không kích hoạt bởi TRUNCATE.
- Ảnh hưởng đến FK.

## ALTER

- Thay đổi cấu trúc của table có sẵn.
- Cho phép add, modify, delete, rename các thành phần của table.

## DROP TABLE

- Xóa cấu trúc và data một bảng.
- 
