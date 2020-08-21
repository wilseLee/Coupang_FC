## 百伦OMS获取订单状态(未实现)

请求方式 | 请求路径
---|---
Get | /apiV2/bailunOrder/queryOrderStatus

## 请求说明

- 参数类型为C#类型，其他语言请自行转换；

## 请求参数(QueryOrderStatusDTO)

```
{
	"originOrderNo":"string"
}
```



## 返回参数(OrderStatusOutput)

```
{
	"originOrderNo":"string",
	"orderStatus":1,
	"trackingNo":"string",
	"lastUpdateTime":"string"
}
```



## 参数说明

#### QueryOrderStatusDTO

| 字段          | 字段类型 | Required | 示例   | 字段说明 |
| ------------- | ---------- | ------ | -------- | -------- |
| OriginOrderNo | string | true | xxxxxx |平台订单号



#### OrderStatusOutput

| 字段          | 字段类型 | Required | 示例   | 字段说明 |
| -------------- | ------------------ | ------------------- | -------------- | -------- |
| OriginOrderNo | string | True | xxxx | 平台订单号         |
| OrderStatus | OrderStatusDTO | True |  | 订单状态         | 
| TrackingNo | string | False | xxxx | 跟踪号（物流单号）    |
| LastUpdateTime | string | True | 2020-01-03 00:00:00 | 最后更新时间(UTC) |



#### OrderStatusDTO（订单状态枚举）

| 枚举              | 说明       | 序号 |
| ----------------- | ---------- | ---- |
| Unpackaged        | 未打包     | 1    |
| Packaged          | 已打包     | 2    |
| GetTrackingNumber | 获取跟踪号 | 3    |
| Shipped           | 已发货     | 4    |
| Error             | 发货失败   | 5    |

