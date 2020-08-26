## 百伦OMS获取订单状态(未实现)

| 请求方式 | 请求路径                            |
| -------- | ----------------------------------- |
| Get      | /apiV2/bailunOrder/queryOrderStatus |

## 请求说明

- 参数类型为C#类型，其他语言请自行转换；

## 请求参数(QueryOrderStatusDTO)

```
{
	"originOrderNo":"string"
}
```



## 返回参数(BaseResponse<OrderStatusOutput>)

```
{
    "result": {
        "originOrderNo": "string",
        "orderStatus": 1,
        "trackingNo": "string",
        "lastUpdateTime": "string",
        "shipFaildType":null,
        "exceptionType":null
    },
    "message": "string",
    "code": 10000
}
```



## 参数说明

#### QueryOrderStatusDTO

| 字段          | 字段说明   | 示例   | 字段类型 | Required |
| ------------- | ---------- | ------ | -------- | -------- |
| OriginOrderNo | 平台订单号 | xxxxxx | string   | true     |



#### BaseResponse（Response parameters）

| Field   | Field description | Example    | Field Type                     | Required |
| ------- | ----------------- | ---------- | ------------------------------ | -------- |
| Result  | 结果集            |            | T（Type of OrderStatusOutput） | false    |
| Message | 返回消息          | 订单不存在 | string                         | false    |
| Code    | 返回状态码        | 10000      | ExternalCode                   | true     |



#### OrderStatusOutput

| 字段           | 字段说明           | 示例                | 字段类型       | Required |
| -------------- | ------------------ | ------------------- | -------------- | -------- |
| OriginOrderNo  | 平台订单号         | xxxx                | string         | True     |
| OrderStatus    | 订单状态           |                     | OrderStatusDTO | True     |
| TrackingNo     | 跟踪号（物流单号） | xxxx                | string         | False    |
| LastUpdateTime | 最后更新时间(UTC)  | 2020-01-03 00:00:00 | string         | True     |
| ShipFaildType  | 发货异常类型       | 1                   | ShipFaildType  | False    |
| ExceptionType  | 订单异常类型       | 2                   | ExceptionType  | False    |



#### OrderStatusDTO（订单状态枚举）

| 枚举              | 说明       | 序号 |
| ----------------- | ---------- | ---- |
| Unpackaged        | 未打包     | 1    |
| Packaged          | 已打包     | 2    |
| GetTrackingNumber | 获取跟踪号 | 3    |
| Shipped           | 已发货     | 4    |
| Error             | 发货失败   | 5    |




#### ExternalCode（状态码枚举）

| 枚举         | 说明         | 序号  |
| ------------ | ------------ | ----- |
| SUCCESS      | 成功         | 10000 |
| ER_PARAMETER | 请求参数异常 | 10001 |
| ER_SYSTEM    | 系统内部异常 | 10010 |



#### ShipFaildType（发货异常类型枚举）

| 枚举                | 说明         | 序号 |
| ------------------- | ------------ | ---- |
| NetworkEx           | 网络问题     | 0    |
| CharacterEx         | 字符问题     | 1    |
| LogisticsEx         | 渠道问题     | 2    |
| PackingEx           | 重量尺寸     | 3    |
| StockEx             | 库存问题     | 4    |
| BalanceEx           | 余额问题     | 5    |
| TakeStock           | 盘点订单     | 6    |
| LgisticsReturn      | 物流退件     | 7    |
| PreentryEx          | 预报异常     | 8    |
| InterceptOrder      | 已拦截订单   | 9    |
| InterceptOrderError | 拦截失败订单 | 10   |
| OtherEx             | 其他问题     | 99   |



#### ExceptionType（订单异常类型枚举）

| 枚举                       | 说明                         | 序号 |
| -------------------------- | ---------------------------- | ---- |
| SkuMapLost                 | sku映射缺失                  | 1    |
| ReceiptAddressError        | 地址识别异常                 | 2    |
| LogisticsUnknown           | 系统匹配不到物流规则         | 4    |
| WareHouseUnknown           | 系统匹配不到仓库规则         | 5    |
| BailunOrder                | 系统匹配到自定义订单问题规则 | 6    |
| PickingApply               | 配货时触发规则拦截订单       | 8    |
| StopPicking                | 人为暂停配货                 | 10   |
| SpecifiedLogisticsUnVerify | 订单指定的物流被禁用         | 11   |
| NoValidLogistics           | 由于物流限制不可用           | 12   |
| NoValidWarehouse           | 指定区域没有发货仓库         | 13   |
| ReceivierPhoneError        | 联系人/电话异常              | 15   |
| LogisticsReturn            | 物流退件单                   | 16   |
| NoOptimalLogistics         | 无法匹配最优物流             | 24   |
| WrongSizeOfProduct         | 产品尺寸错误                 | 25   |
| CreateApply                | 创建配货单时发生异常         | 27   |

