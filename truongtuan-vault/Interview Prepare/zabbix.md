## Integrate Zabbix API
Tich hợp Zabbix Connector Module gọi đến API zabbix.
1. Vấn đề giải quyết:
	1. Code base dùng cho call zabbix API.
	2. Tránh việc douplicate code.
	3. Tái sử dụng.
	4. Đảm bảo nhất quán convention.
2. Triển khai:
	1. Create zabbix dto class that for map zabbix response.
	2.  Implement generic based on Reponse Dto.
	3. Based on Webclient from Spring WebFlux.
	4. Implement API key provider that can load api from redis or database corresponding to the login user. 
## Create base service
1. The generic service based on Response DTO that provide default API call like:get, create, update, delete.
2. Java generic, Default method.

**Report**
- API expose api to client
- code: common dto entity
- facade: as service orchrestrator
- ExportRequest: user, apid, context (export param)
1. make request
	1. save db with inprocess
	2. sed to kafka topic
2. consume request by Report Worker
	1. parse request context as export request query
	2. pass to datasetprovider
	3. export to excel then save to minio

