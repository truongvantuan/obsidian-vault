### Basic Questions

1. **What is Spring Data JPA?**
	
    - Explain what Spring Data JPA is and its primary purpose.
    - 
1. **What are the key features of Spring Data JPA?**
    
    - Discuss features like repository abstraction, CRUD operations, and the domain-specific language.
    - Repository abstruction.
1. **What is a repository in Spring Data JPA?**
    
    - Define what a repository is and its use in data access layers.
4. **Explain the difference between CrudRepository, JpaRepository, and PagingAndSortingRepository.**
    
    - Describe the functionalities and differences between these interfaces.
5. **What is the purpose of the `@Entity` annotation in JPA?**
    
    - Explain why and where you'd use the `@Entity` annotation.
6. **How do you define primary keys in JPA?**
    
    - Discuss `@Id`, `@GeneratedValue`, and their strategies.
7. **What are JPQL and its advantages?**
    
    - Describe the Java Persistence Query Language and its use cases.
8. **How do you paginate results in Spring Data JPA?**
    
    - Explain the use of `Pageable` and `Page` interfaces for pagination.

### Intermediate Questions

1. **What is the purpose of the `@Query` annotation?**
    
    - Discuss custom queries and when you would use the `@Query` annotation.
2. **How do you perform a join query in Spring Data JPA?**
    
    - Provide examples of how to write join queries using JPQL or the `@Query` annotation.
3. **What are named queries in JPA and how do you define them?**
    
    - Explain named queries and their definition using the `@NamedQuery` annotation.
4. **What is optimistic locking, and how do you implement it in Spring Data JPA?**
    
    - Discuss the concept of optimistic locking and how to use the `@Version` annotation.
5. **Explain the purpose of the `@Modifying` annotation.**
    
    - Describe scenarios where you need to use the `@Modifying` annotation.
6. **How do you handle transactions in Spring Data JPA?**
    
    - Discuss the `@Transactional` annotation and transaction management.
7. **What is the difference between `fetch` and `lazy` loading?**
	- Resolve:
		1. JOIN FETCH
		2. Entity graphs
		3. Batch fetch config
		4. Using eager
    - Explain the differences between these loading strategies with examples.
9. **What is the role of `[EntityManager](code_navigation_link_20)` in JPA?**
    
    - Describe the functionality and use cases of `[EntityManager](code_navigation_link_20)`.

### Advanced Questions

1. **How do you configure multiple data sources in Spring Data JPA?**
    
    - Explain the steps to configure and manage multiple data sources.
2. **What are entity listeners and how do you use them?**
    
    - Discuss the lifecycle callbacks and how to use entity listeners.
3. **How do you manage relationships (OneToMany, ManyToOne, ManyToMany) in JPA?**
    
    - Explain mappings with examples and use cases.
4. **What strategies can you use to address N+1 select problems in JPA?**
    
    - Discuss techniques and annotations like `@EntityGraph` and `JOIN FETCH`.
5. **What is the purpose of `Criteria API` in JPA?**
    
    - Explain the Criteria API and scenarios where it is beneficial.
6. **How do you integrate Spring Data JPA with other Spring modules like Spring Security?**
    
    - Discuss configuration and practical use cases.
7. **Explain how caching works in JPA.**
    
    - Cover the second-level cache and how to enable/disable caching.
8. **Describe how to handle batch processing in Spring Data JPA.**
    
    - Discuss strategies and configurations for batch inserts and updates.