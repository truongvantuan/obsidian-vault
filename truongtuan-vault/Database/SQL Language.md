## GROUP BY

`GROUP BY` là mệnh đề dùng để `nhóm các rows` có `cùng giá trị` `tại một hoặc nhiều column khác nhau.`
`GROUP BY` thường được dùng với các hàm tổng hợp (aggregate function) như `SUM, MAX, MIN, COUNT, AVG`.

Tính năng chính của `GROUP BY`:
- Nhóm các rows: group các row có giá trị cột của cột chỉ định giống nhau thành một group.
- Yêu cầu hàm tổng hợp: Data tại group được tổng hợp bởi các hàm tổng hợp.
- Vấn đề về order: `GROUP BY` được áp dụng trước khi hàm tổng hợp xử lý data, nó hoạt động độc lập với `ORDER BY`.
- Column selection: tất cả các column trong `SELECT` phải tuần thủ:
	1. Nằm trong hàm tổng hợp kết quả, hoặc:
	2. Được nằm trong mệnh đề `GROUP BY`
## SELECT

**SELECT** statement có các mệnh đề sau:
1. Chọn các row riêng biệt với **DISTINCT**
2. Sắp xếp row với **ORDER BY**
3. Lọc row với **WHERE**
4. Chọn subset của kết quả SELECT với **LIMIT** hoặc **FETCH**
5. Nhóm row vào các group với **GROUP BY**
6. Lọc GROUP với **HAVING**
7. Join các bảng khác nhau với JOIN, LEFT JOIN, RIGHT JOIN,...
8. Kết hợp kết quả từ nhiều câu SELECT với UNION, INTERSECT và EXCEPT.
	1. UNION kết hợp kết quả và loại bỏ trùng lặp.
	2. INTERSECT tìm kết quả chung giữa các kết quả từ SELECT.
	3. EXCEPT lấy kết quả có trong select 1 và không có trong select 2.

