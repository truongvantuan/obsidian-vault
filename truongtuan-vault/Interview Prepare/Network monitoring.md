Good afternoon everyonce.
Thank you for giving me the opportunity to interview for this position.
My name is Tuan, and I am a Java Web developer with 3 years of experience.
I have a background for develop web application on several fields like banking, booking portal, netwoking.
In my most recent role at NGSC, I worked on developing scalable Java applications, integrating with various APIs.
# Custom R2DBC repository
## Vấn đề gặp phải
1. Cần đảm tính nhất quán cho fully reactive programming trên toàn bộ ứng dụng. Cần thiết sử dụng R2DBC + PostgreSQL.
2. Spring Data R2DBC limitations:
	1. No relationship: không thể tạo quan hệ các bảng phía Entity.
	2. Limited Object mapping: chỉ hỗ trợ ánh xạ field với column.
	3. Schema management: không có khả năng ánh dạ thay đổi từ Entity đến Table.
	4. 
3. Cần các tính năng:
	1. Type-safe query API.
	2. Readable and Maintainable code: fluent style coding.
	3. Hỗ trợ build query phức tạp, sub-query, join.
	4. Custom Repository Interface pass Function: cho phép viết functional programming (triển khai tại thời điểm code), phù hợp với reactive programming.
## R2dbcRepositoryFactoryBean

#### 1: Implement repo interface
1. Define generic repository fragment with methods.
2. Implement repository fragment based on QueryDSL:
	1. Start with SQLQueryFactory
	2. Tùy thuộc vào query, update, delete -> SQLQuery, SQLUpdateClause, SQLDeleteClause:
		1. sqlQueryFactory.query()
		2. sqlQueryFactory.update(path)
		3. sqlQueryFactory.delete(path).where(predicate);
	3. Có SQL String, có Binding objects
	4. Pass to binder class: postgresql sử dụng index kiểu $1.
		1. Bind là quá trình đưa sql query string từ QueryDSL sang tương thích với databaseclient. Tức đưa place holder từ ? sang $1, P0_0 tùy thuốc database driver.

#### 2: Integrate into spring data

`@EnableR2dbcRepositories(repositoryFactoryBeanClass = QuerydslR2dbcRepositoryFactoryBean.class)`
- Annotation cung cấp khả năng chỉ định RepositoryFactoryBean -> mở rộng R2dbcRepositoryFactoryBean.class

1. Mở rộng R2dbcRepositoryFactory.
2. Gi đè method getRepositoryFragments(RepositoryMetadata metadata).
3. Đưa repo fragment đã implement vào 2: fragments.append(querydslJdbcFragment).