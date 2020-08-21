## OMS推送订单接口(未实现)
请求方式 | 请求路径
---|---
POST| /api/order/createOrder

  

## 请求说明

- 参数类型为C#类型，其他语言请自行转换；
- 创建订单后，后续再次推送只更新订单，+平台单号（OriginOrderNo）为唯一要素，请确保正确性；

## 请求参数（OrderCreateForExternal）

```json
{
  "originOrderNo": "string",
  "lastUpdateTimeUtc": "2020-08-13T08:46:09.196Z",
  "receiptAddress": {
	"countryCode":"string",
	"country":"string",
    "stateOrRegion": "string",
    "city": "string",
    "address": "string",
    "address2": "string",
	"postalCode":"string"
    "receiver": "string",
    "phone": "string",
    "phone2": "string"
  },
  "platSkuItems": [
    {
      "skuNo": "string",
      "title": "string",
      "itemId": "string",
      "quantityOrdered": 0,
      "unitPrice": {
        "amount": 0,
        "currencyCode": "string"
      }
    }
  ]
}
```

## 返回参数（OrderForExternalOutput）

```json
{
  "message": "string",
  "code": 10000
}
```



## 参数说明

#### OrderCreateForExternal（订单创建DTO）

| 字段                | 字段说明                 | 示例                | 字段类型               | Required |
| :------------------ | :----------------------- | ------------------- | :--------------------- | -------- |
| OriginOrderNo       | 原始订单号,平台单号      | 32000064249278      | string                 | true     |
| LastUpdateTimeUtc   | 最后更新时间(UTC)             | 2020-02-02 08:15:30 | DateTime               | true     |
| ReceiptAddress      | 收货地址                 |                     | ReceiptAddress         | true     |
| PlatSkuItems        | sku信息                  |                     | List<PlatSkuItemInput> | true     |


#### ReceiptAddress（收货地址）

| 字段          | 字段说明   | 示例                                  | 字段类型 | Required |
| ------------- | ---------- | ------------------------------------- | -------- | -------- |
| CountryCode   | 国家二字码 | KR                                    | string   | true     |
| Country       | 国家       | Korea                                 | string   | false    |
| StateOrRegion | 州省       | 경기도                                | string   | true     |
| City          | 城市       | 수원시                                | string   | true     |
| Address       | 地址1      | 장안구 천천동 482 비단마을 신명아파트 | string   | true     |
| Address2      | 地址2      | 753-xxx                               | string   | false    |
| PostalCode    | 邮编       | 16323                                 | string   | true     |
| Receiver      | 收件人姓名 | xxx                                   | string   | true     |
| Phone         | 联系电话   | 0503-809x-xxxx                        | string   | true     |
| Phone2        | 联系电话1  |                                       | string   | false    |



#### PlatSkuItemInput（sku详情）

| 字段            | 字段说明               | 示例                                                         | 字段类型 | Required |
| --------------- | ---------------------- | ------------------------------------------------------------ | -------- | -------- |
| SkuNo           | SKU编号                | 942702003                                                    | string   | true     |
| Title           | 标题                   | 여성의 섹시한 깊은 V 넥 이브닝 드레스 스팽글 민소매 드레스 큰 스윙 스커트, L, Purple | string   | true     |
| ItemId          | ItemId（商品链接的ID） | 5430020770                                                   | string   | true     |
| QuantityOrdered | 下单数量               | 1                                                            | int      | true     |
| UnitPrice       | 单价                   |                                                              | MoneyDTO | true     |


#### MoneyDTO（金额DTO）

| 字段         | 字段说明 | 示例 | 字段类型 | Required |
| ------------ | -------- | ---- | -------- | -------- |
| Amount       | 金额     | 10   | decimal  | true     |
| CurrencyCode | 货币单位 | KRW  | string   | true     |



#### OrderForExternalOutput（返回参数）

| 字段    | 字段说明 | 示例         | 字段类型     | Required |
| ------- | -------- | ------------ | ------------ | -------- |
| Message | 返回信息 | 创建订单成功 | string       | false    |
| Code    | 返回代码 | 10000        | ExternalCode | true     |




#### ExternalCode（状态码枚举）

| 枚举         | 说明         | 序号  |
| ------------ | ------------ | ----- |
| SUCCESS      | 创建成功     | 10000 |
| ER_PARAMETER | 请求参数异常 | 10001 |
| ER_SYSTEM    | 系统内部错误 | 10010 |
| ER_NotFoundSKU    | 商品SKU未找到 | 11000 |
