
## KAFKA_BROCKER_ID

- Gán một ID duy nhất cho Brocker trong Kafka Cluster.
- Giúp xác định Broker trong cụm.

## KAFKA_LISTENER


## KAFKA_LISTENER_SECURITY_PROTOCOL_MAP

**Syntax:**
`<Listener-Name>:<Security-Protocol>,<Listener-Name>:<Security-Protocol>,...`

- Giúp cấu hình giao thức bảo mật cho Kafka listener.
- Giao thức bảo mật (security protocol) xác định cách các client, controller, brocker giao tiếp với nhau.
- **Listener-Name**:
	- Giá trị được khai báo trong biến KAFKA_LISTENERS
- **Security-Protocol**: giao thức bảo mật, thuộc một trong các giá trị sau.
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

**Syntax**:
`KAFKA_ADVERTISED_LISTENERS=<listener_name>://<hostname>:<port>[,<listener_name>://<hostname>:<port>,...]`
- Yêu cầu ít nhất một giá trị.
- <listener_name>
	- Logical name để xác định listener.
	- Phải được khai báo tại KAFKA_LISTENERS.
- <host_name>
	- DNS name hoặc địa chỉ IP mà client sử dụng để kết nối đến brocker.
	- Thường là địa chỉ external IP hoặc hostname có thể truy cập bởi client.
- \<port>