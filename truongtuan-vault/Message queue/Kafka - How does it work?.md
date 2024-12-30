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


## Zookeeper
46

[](https://stackoverflow.com/posts/48652680/timeline)

> I am going to implement the orchestration of a set of microservices in my application.

This is a hard problem to solve by yourself. You are probably better off using an existing orchestration system (see below).

> Is there any other powerful tool?

You should look into kubernetes, which seems to be the standard in orchestration these days. It has many additional benefits (enable scalability, self-healing, etc) and is widely used in production today. See the following links:

- [Kubernetes webpage](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)
- [Article](https://www.stratoscale.com/blog/kubernetes/container-orchestration-kubernetes-12-key-features/)

Regarding comparing zookeeper, eureka and kubernetes:

- [Zookeeper](https://zookeeper.apache.org/) is a distributed key value store. It can be used as the basis to implement service discovery (similar to etcd).
- [Eureka](https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance) is primarily a service locator used as part of Netflixes load balancers and failover(allow finding the right service targets for distributing client calls to members of an application cluster).
- [Kubernetes](https://kubernetes.io/) is a container orchestration solution that includes the deployment, discovery and self-healing of services. For a complete list of features, check the link above. The service discovery in kubernetes is based on dns in the virtual network it spans and builds upon etcd.
- [Consul](https://github.com/hashicorp/consul) (mentioned in the other answer) is a service discovery framework with a REST interface and some additional features (Health Checking, Service Segmentation,..). It has its own internal distributed key value store that can be used as well.