## OMS gets order status (Not implemented)

Request method | Request path
---|---
Get | /apiV2/bailunOrder/queryOrderStatus

## Request description

- The parameter type is C#, please convert other languages by yourself;

## Request parameter(QueryOrderStatusDTO)

```
{
	"originOrderNo":"string"
}
```



## Response parameters(OrderStatusOutput)

```
{
	"originOrderNo":"string",
	"orderStatus":1,
	"trackingNo":"string",
	"lastUpdateTime":"string"
}
```



## Parameter Description

#### QueryOrderStatusDTO

| Field          | Field Type | Required | Example   | Field description |
| ------------- | ---------- | ------ | -------- | -------- |
| OriginOrderNo | string | true | xxxxxx |Platform order number



#### OrderStatusOutput

| Field          | Field Type | Required | Example   | Field description |
| -------------- | ------------------ | ------------------- | -------------- | -------- |
| OriginOrderNo | string | True | xxxx | Platform order number         |
| OrderStatus | OrderStatusDTO | True |  | Order Status         | 
| TrackingNo | string | False | xxxx | Tracking Number (Logistic Number)   |
| LastUpdateTime | string | True | 2020-01-03 00:00:00 | Last update time(UTC) |



#### OrderStatusDTO（Order status enum）

| value              | Description       | Serial number |
| ----------------- | ---------- | ---- |
| Unpackaged        | Unpackaged     | 1    |
| Packaged          | Packaged     | 2    |
| GetTrackingNumber | Get tracking number | 3    |
| Shipped           | Shipped     | 4    |
| Error             | Delivery failed   | 5    |

