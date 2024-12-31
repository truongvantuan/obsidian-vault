
## KAFKA_BROCKER_ID

- Gán một ID duy nhất cho Brocker trong Kafka Cluster.
- Giúp xác định Broker trong cụm.
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
> 