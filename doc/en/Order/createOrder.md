## OMS Push order Api(Not implemented)

| Request method | Request path           |
| -------------- | ---------------------- |
| POST           | /api/order/createOrder |

## Request description

- The parameter type is C# type, please convert other languages by yourself.
- After the order is created, the subsequent push will only update the order, and the platform order number (OriginOrderNo) is the only element, please ensure that it is correct.

## Request parameter（OrderCreateForExternal）

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
	"postalCode":"string",
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

## Response parameter（BaseResponse）

```json
{
  "message": "string",
  "code": 10000
}
```



## Parameter Description

#### OrderCreateForExternal（Order creation DTO）

| Field             | Field description                            | Example             | Field Type             | Required |
| :---------------- | :------------------------------------------- | ------------------- | :--------------------- | -------- |
| OriginOrderNo     | Original order number(platform order number) | 32000064249278      | string                 | true     |
| LastUpdateTimeUtc | Last update time(UTC)                        | 2020-02-02 08:15:30 | DateTime               | true     |
| ReceiptAddress    | Shipping address                             |                     | ReceiptAddress         | true     |
| PlatSkuItems      | sku information                              |                     | List<PlatSkuItemInput> | true     |


#### ReceiptAddress（Shipping address DTO）

| Field         | Field description    | Example                               | Field Type | Required |
| ------------- | -------------------- | ------------------------------------- | ---------- | -------- |
| CountryCode   | Country code         | KR                                    | string     | true     |
| Country       | Country              | Korea                                 | string     | false    |
| StateOrRegion | province / State     | 경기도                                | string     | true     |
| City          | city                 | 수원시                                | string     | true     |
| Address       | Address 1            | 장안구 천천동 482 비단마을 신명아파트 | string     | true     |
| Address2      | Address 2            | 753-xxx                               | string     | false    |
| PostalCode    | Postcode             | 16323                                 | string     | true     |
| Receiver      | The recipient's name | xxx                                   | string     | true     |
| Phone         | contact number       | 0503-809x-xxxx                        | string     | true     |
| Phone2        | Contact number 1     |                                       | string     | false    |



#### PlatSkuItemInput（sku details DTO）

| Field           | Field description         | Example                                                      | Field Type | Required |
| --------------- | ------------------------- | ------------------------------------------------------------ | ---------- | -------- |
| SkuNo           | SKU number                | 942702003                                                    | string     | true     |
| Title           | title                     | 여성의 섹시한 깊은 V 넥 이브닝 드레스 스팽글 민소매 드레스 큰 스윙 스커트, L, Purple | string     | true     |
| ItemId          | ItemId（Product link ID） | 5430020770                                                   | string     | true     |
| QuantityOrdered | Order quantity            | 1                                                            | int        | true     |
| UnitPrice       | unit price                |                                                              | MoneyDTO   | true     |


#### MoneyDTO（Amount DTO）

| Field        | Field description | Example | Field Type | Required |
| ------------ | ----------------- | ------- | ---------- | -------- |
| Amount       | Amount            | 10      | decimal    | true     |
| CurrencyCode | Currency Unit     | KRW     | string     | true     |



#### BaseResponse（Response parameters）

| Field   | Field description        | Example                    | Field Type   | Required |
| ------- | ------------------------ | -------------------------- | ------------ | -------- |
| Result  | Return result set if any |                            | object       | false    |
| Message | returned messages        | Successfully created order | string       | false    |
| Code    | Return code              | 10000                      | ExternalCode | true     |




#### ExternalCode（Status code enumeration）

| enumerate    | Description                 | Serial number |
| ------------ | --------------------------- | ------------- |
| SUCCESS      | Created successfully        | 10000         |
| ER_PARAMETER | Request parameter exception | 10001         |
| ER_SYSTEM    | Internal System Error       | 10010         |
