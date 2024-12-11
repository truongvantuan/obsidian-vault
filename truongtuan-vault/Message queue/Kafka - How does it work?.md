## Kafka architecture

- Kafka hoạt động như là pub-sub message middleware.
- Kafka có thành phần chính:
	- producer: gửi message.
	- broker: handle tin nhắn đến và ghi vào broker partitions, cho phép consumer đọc các message từ đây.
	- consumer: nhận tin nhắn.
- Kafka được đinh vị như là event streaming platform.

## Compute layer

> Cho phép các nền tảng ứng dụng giao tiếp với Kafka broker thông qua API.

- Producer sử dụng Producer API, nếu là Database thì sử dụng Kafka Connect.

## Storage layer

## Basic of Topic and Partition.
1. Topic: logical grouping of messages, các message được gom nhóm theo một logic nào đó.
2. Partition:
	1. Mỗi một topic được chia thành một hoặc nhiều partition cho việc đống thời và mở rộng.
	2. Một message được lưu trên một partition, không trùng lặp giữa các partitions.
	3. Partitions được đặt theo thứ tự.
Khi một message được gửi đi, Kafka sẽ quyết định partition nào nắm giữ message.
```
Partition 0: [Message 1, Message 4, Message 7]  
Partition 1: [Message 2, Message 5]  
Partition 2: [Message 3, Message 6]
```

## Message được chưa vào Partition như thế nào.

