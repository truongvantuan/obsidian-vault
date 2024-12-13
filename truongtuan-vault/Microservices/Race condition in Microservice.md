## Database-Level Synchronization

- Sử dụng @Version lên entity.
- Sử dụng @Lock lên JPA method, lúc này các transaction khác không thể đọc ghi lên record đang bị khóa cho đến khi transaction hoàn thành.
```java
   @Lock(LockModeType.PESSIMISTIC_WRITE)
   @Query("SELECT a FROM Account a WHERE a.id = :id")
   Optional<Account> findAccountForUpdate(@Param("id") Long id);
```

## Application-Level Synchronization

> Triển khai code đảm bảo thread-safe, các cơ chế blocking để quản lý cho các critical section.
- Synchronized
- Lock từ Java Concurrency
## Distributed Locking (Microservices)

> Race condition có thể xẩy ra khi nhiều instance của một service thao tác lên cùng một tài nguyên.

1. Redisson
```java
@Service
public class RedisLockService {

    @Autowired
    private RedissonClient redissonClient;

    public void performTaskWithLock() {
        RLock lock = redissonClient.getLock("resource_lock");
        try {
            if (lock.tryLock(10, 100, TimeUnit.SECONDS)) {
                // Critical section
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        } finally {
            lock.unlock();
        }
    }
}
```
`String lockKey = "product_sync_lock_" + key.getProductId();`

2. Event -Driven architecture
> Thiết kế kiến trúc sao cho các services giao tiếp thông qua event.
- Đảm bảo xử lý message theo idempotency.
3. Transaction management
	1. ads
## Prevent concurrent request

