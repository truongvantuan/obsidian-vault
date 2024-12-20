## @RetryableTopic

> Sử dụng cho **message reties** và **failure processing**

1. Quá trình xử lý message có thể tạm thời lỗi do:
	1. Network hoặc Database ngừng hoạt động.
	2. API timeout hoặc lỗi.
	3. Tắc nghẽn tạm thời trong nội tại ứng dụng. 
	Thay vì hủy bỏ hoặc gửi message tới Dead-Letter-Topic @RetryableTopic cho phép retry message lỗi, hoặc delay việc xử lý message trong khoảng thời gian có thế cấu hình.
2. Tránh mất mát giữ liệu (message), không triển khai cơ chế retry, message lỗi có thể:
	1. Bị mất nếu Dead Letter Queue không được sử dụng.
	2. Ngay lập tức được gửi đến DLQ, trong khi sự cố có thể được xử lý sau khi được retry.
	@RetryableTopic đảm bảo message lỗi được retry, giúp giảm việc message bị mất và chỉ gửi đến DLQ sau khi message dã được retry lỗi.
3. Cấu hình retry linh hoạt.
	1. Number of Retry Attempts: số lần thử lại trước khi message được gửi tới DLQ.
	2. Backoff Strategy: đỗ trễ giữa các lần retry.
	3. Excluding Exception: xác định ngoại lệ cho retry và gửi đến DLQ khi gặp.
4. 

Example:
```java
@Documented  
@RetryableTopic  
@Target({ElementType.METHOD, ElementType.ANNOTATION_TYPE, ElementType.TYPE})  
@Retention(RetentionPolicy.RUNTIME)  
public @interface RetrySupportDql {  
    @AliasFor(annotation = RetryableTopic.class, attribute = "backoff")  
    Backoff backoff() default @Backoff(value = 6000);  
    @AliasFor(annotation = RetryableTopic.class, attribute = "attempts")  
    String attempts() default "4";  
    @AliasFor(annotation = RetryableTopic.class, attribute = "autoCreateTopics")  
    String autoCreateTopics() default "true";  
    @AliasFor(annotation = RetryableTopic.class, attribute = "listenerContainerFactory")  
    String listenerContainerFactory() default "";  
    @AliasFor(annotation = RetryableTopic.class, attribute = "exclude")  
    Class<? extends Throwable>[] exclude() default {};  
    @AliasFor(annotation = RetryableTopic.class, attribute = "sameIntervalTopicReuseStrategy")  
    SameIntervalTopicReuseStrategy sameIntervalTopicReuseStrategy() default SameIntervalTopicReuseStrategy.SINGLE_TOPIC;  
}
```

- RetrySupportDql đánh dấy mở rộng @RetryableTopic
