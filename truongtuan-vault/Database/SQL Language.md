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
