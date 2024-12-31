## "---" character trong file Application.yaml
1. Sử dụng phân chia file thành nhiều phần giúp khai báo nhiều Profile trong một file.
2. Global config được khai báo trước "---" đầu tiên.
## Just one application.yaml
1. `spring.profiles.active=dev` : xác định profile active mặc định.
2. `spring.config.activate.on-profile=dev` : cấu hình được merge vào global config.
3. Spring boot ưu tiên (ghi đè) khai báo tại profile cụ thể nếu trùng key.
4. Khai báo không chỉ rõ `on-profile` sẽ áp dụng cho global.
