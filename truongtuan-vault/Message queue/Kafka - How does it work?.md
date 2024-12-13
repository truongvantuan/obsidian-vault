## Kafka architecture

- Kafka hoạt động như là pub-sub message middleware.
- Kafka có thành phần chính:
	- producer: gửi message.
	- broker: handle tin nhắn đến và ghi vào broker partitions, cho phép consumer đọc các message từ đây.
	- consumer: nhận tin nhắn.
- Kafka được đinh vị (positioned) như là event streaming platform.

## Compute layer

> Cho phép các nền tảng ứng dụng giao tiếp với Kafka broker thông qua API.

- Producer sử dụng Producer API.
- Consumer sử dụng Consumer API.
- Nếu là Database thì sử dụng Kafka Connect.

## Storage layer


## Basic of Topic and Partition.
1. Topic: logical grouping of messages, các message được gom nhóm theo một logic nào đó.
2. Partition:
	1. Mỗi một topic được chia thành một hoặc nhiều partition cho việc đống thời và mở rộng.
	2. Một message được lưu trên một partition, không trùng lặp giữa các partitions.
	3. Partitions được đặt theo thứ tự.
Khi một message được gửi đi, Kafka sẽ quyết định partition nào nắm giữ message.

## Message được chưa vào Partition như thế nào.

1. Message with no key:
	1. Message sẽ được phân bố đều tuần tự trên các partitions: round-robin.
```
Partition 0: [Message 1, Message 4, Message 7]  
Partition 1: [Message 2, Message 5]  
Partition 2: [Message 3, Message 6]
```
2. Dựa vào message key.
**partition = hash(key) % number_of_partitions**
	1. Kafka hash giá trị key để đưa message vào partition.
	2. Message cùng key sẽ vào cùng partition.
	3. Đảm bảo thứ tự message đưa vào và lấy ra.
4. Custom partitioning logic:
```java
// Custom partitioning logic  
public class CustomPartitioner implements Partitioner {  
    @Override  
    public int partition(String topic, Object key, byte[] keyBytes, Object value, byte[] valueBytes, Cluster cluster) {  
        // Direct all "priority" messages to Partition 0  
        if ("priority".equals(key)) {  
            return 0;  
        } else {  
            // Default partitioning for other messages  
            return key.hashCode() % cluster.partitionCountForTopic(topic);  
        }  
    }  
}
```

## Message key strategy

1. Without a Key
	1. Stateless message.
	2. Cân bằng tải tốt.
	3. Dễ cấu hình.
	4. Thích hợp cho stateless message: các message độc lập, không yêu cầu thứ tự message.
	5. Logging, metric, transaction event.
3. With a Key
	1. Stateful message.
	2. Đảm bảo thứ tứ message cùng key.
	3. Xử lý parallel hiệu quả: Các message cùng chung logic được gom nhóm theo partition. Dễ dàng xử lý parallel phía consumer. Example: order theo từng khách hàng sẽ được xử lý song song cùng lúc.

## Consumer Group
