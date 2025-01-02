
## Thuật ngữ

1. Kafka Client:
	1. External Clients:
		- Là các client bên ngoài Kafka tham gia vào việc kết nối, sử dụng và tương tác với Broker như: Producer, Consumer, Microservice, Ứng dụng.
		- Kết nối với Kafka Broker thông qua địa chỉ được khai báo tại [[#KAFKA_ADVERTISED_LISTENERS]]
	1. Internal Clients:
		- Là các thành phần thuộc về Kafka cluster infrastructure.
		- Kafka broker: Inter-Broker communication
		- Controller
		- Repllication Traffic
---
**Example**
```yml
services:  
  broker:  
    image: apache/kafka:latest  
    hostname: broker  
    container_name: broker  
    ports:  
      - "9092:9092"  
    environment:  
      # Broker identity and Initialization variables  
      KAFKA_BROKER_ID: 1  
      KAFKA_NODE_ID: 1  
      CLUSTER_ID: MkU3OEVBNTcwNTJENDM2Qk  
      KAFKA_PROCESS_ROLES: broker,controller  
      # Listener configuration  
      KAFKA_LISTENERS: PLAINTEXT://broker:29092,CONTROLLER://broker:29093,PLAINTEXT_HOST://0.0.0.0:9092 
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://broker:29092,PLAINTEXT_HOST://localhost:9092  
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT,CONTROLLER:PLAINTEXT  
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT  
      KAFKA_CONTROLLER_LISTENER_NAMES: CONTROLLER  
      # Controller configuration  
      KAFKA_CONTROLLER_QUORUM_VOTERS: 1@broker:29093  
      # Topic and Partition management  
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1  
      KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS: 0  
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 1  
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 1  
      # Log Configuration  
      KAFKA_LOG_DIRS: /tmp/kraft-combined-logs
```
## KAFKA_BROCKER_ID

- Gán một ID duy nhất cho Brocker trong Kafka Cluster.
- Giúp xác định Broker trong cụm.

## KAFKA_LISTENER

> Là một cấu hình quan trong cho Kafka Broker, là địa chỉ Kafka Broker sẽ lắng nge các kết nối khác nhau từ trong à ngoài kafka cluster.

**Syntax**
`KAFKA_LISTENERS: <Listener_Name>://<Host_Name>:<Port>[,<Listener_Name>://<Host_Name>:<Port>,...]`

- Nó cho phép **phân đoạn lưu lượng truy cập** (segmentation of traffic) theo mục đích (ví dụ: external vs internal communication).
- Đảm bảo rằng các nhà môi giới được hiển thị đúng cách trong môi trường mạng như Docker hoặc Kubernetes.
- Hỗ trợ nhiều loại kết nối bằng cách cho phép nhiều người nghe với các giao thức khác nhau (ví dụ: văn bản gốc, SSL, SASL).
- Cung cấp tính linh hoạt để xử lý các tình huống triển khai phức tạp, như môi trường nhiều mạng hoặc cân bằng tải.


## KAFKA_LISTENER_SECURITY_PROTOCOL_MAP

**Syntax:**
`<Listener-Name>:<Security-Protocol>,<Listener-Name>:<Security-Protocol>,...`

- Giúp cấu hình giao thức bảo mật cho Kafka listener.
- Giao thức bảo mật (security protocol) xác định cách các client, controller, brocker giao tiếp với nhau.
- `<Listener-Name>`:
	- Giá trị được khai báo trong biến KAFKA_LISTENERS
- ```<Security-Protocol>```:
	- giao thức bảo mật, thuộc một trong các giá trị sau.
	- PLAINTEXT: không mã hóa, không xác thực. Là cấu hình mặc định của Kafka.
	- SSL: mã hóa giao tiếp thông qua TLS/SSL.
	- SASL_PLAINTEXT: Xác thực nhưng không mã hóa.
	- SASL_SSL: Xác thực và mã hóa.

## KAFKA_ADVERTISED_LISTENERS

> Là một config quan trọng của Kafka khi triển khai Kafka lên Docker, Kubernetes, hoặc môi trường phân tán.
> Giúp cấu hình địa chỉ và cổng (address/port) cho phép clients kết nối đến Brocker.

Biến này chỉ định một Địa chỉ bên ngoài (external address), địa chỉ này được Kafka brocker đưa cho Clients khi Clients yêu cầu Metadata (các thông tin về topic và partition).
- Đặc biệt quan trọng trong môi trường mà ở đó Kafka được triển khai trong Container hoặc NAT (Docker, K8s).
- Không cấu hình đúng dẫn đến clients có thể không kết nối được đến Kafka.

**Best Practice**
- Khai báo cho Inter-Broker comunication tại cổng 29092
- Khai báo address cho External Client tại cổng 9092.

**Syntax**:
`KAFKA_ADVERTISED_LISTENERS=<listener_name>://<hostname>:<port>[,<listener_name>://<hostname>:<port>,...]`
- Yêu cầu ít nhất một giá trị.
- <listener_name>
	- Logical name để xác định listener.
	- Phải được khai báo tại [[#KAFKA_LISTENER]].
- <host_name>
	- DNS name hoặc địa chỉ IP mà client sử dụng để kết nối đến brocker.
	- Thường là địa chỉ external IP hoặc hostname có thể truy cập bởi client.
- \<port>
	- Cổng nơi Listener lắng nghe kết nối từ Client.

**Cách client chọn đúng địa chỉ Listener.**
1. Metadata từ Broker.
	- Khi 1 client kết nối đến Kafka, ban đầu client sẽ sử dụng Bootstrap address (e.g., localhost:9092)
	- Client này sẽ gửi yêu cầu metadata đến Broker.
2. Được trả về Metadata có chưa Advertised Listeners.
	- Response trả về từ Kafka chứa Adversited Listener Address của tất cả Broker trong Cluster.
	- Là các giá trị được khai báo tại Env `KAFKA_ADVERTISED_LISTENERS`.
3. Client Listener matching
	- Client chọn Listener nào để kết nối dựa vào cách client đã được cấu hình ban đầu (initially configured).