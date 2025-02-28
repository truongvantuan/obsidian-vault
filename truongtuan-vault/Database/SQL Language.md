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

### Cấu trúc SELECT

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

### Syntax SELECT

```sql
SELECT
   select_list
FROM
   table_name;
```

- PostegreSQL thức tự xử lý từ FROM trước SELLECT.
- `SELECT <list_select>`
	- List select có thể là column, danh sách columns, expression, literal values.
- `FROM <source_table>`
	- FROM clause là optional.
- SQL keywords là case-insensitive
- `SELECT *`
	- Database performance: lấy về nhiều data hơn cần thiết.
	- Application performance: retrieve data không cần thiết làm tăng traffic giữ DB server và Application Server. Làm giản thời gian phản hồi và khả năng scale ứng dụng.
### Column alias

> Column Alias cho phép gán các thành phần trong SELECT list vào biến tạm.
> Alias chỉ tồn tại tạm tời trong lúc thực thi câu lệnh.

- Alias chứa space `AS "FULL NAME"`

## ORDER BY

![[Pasted image 20250228104243.png]]

> ORDER BY dùng để sắp xếp kết quả trả về từ câu SELECT.
> Sắp xếp ASCENDING/DESCENDING/SORT EXPRESSION

### Syntax

``` sql
ORDER BY
  sort_expression1 [ASC | DESC],
  sort_expression2 [ASC | DESC],
  ...;
```

- Sort multi column: lần lượt sort kết quả từ trái sang phải danh sách sort. Sort sau lấy kết quả sort trước để sắp xếp.
- 