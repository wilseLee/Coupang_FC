## Purchase order
Request method | Request path
---|---
|Post | /api/purchase/service/createPurchaseOrder

## Request header description
Need to add token information, token comes from oauth authorization service

# Input parameter description
Field | Type | Required | Description
---|---|---|---
poNumber|string|true|Purchase Order No
trackingBarCode|string|true|Logistics tracking barcode (used to scan the code offline)
remark|string|false|Order remarks
orderId|string|true|order number
arrivalDate|date|true|Estimated arrival date to the warehouse
skudetails|List&lt;skudetail&gt;|true|sku details

## skudetail DTO Field description
Field | Type | Required | Description
---|---|---|---
sku|string|true|sku code
count|int|true|number of sku



## Response field description
Field | Type | Description
---|---|---
code|int|Request return status code|
message|string|Request message|


## Description of the response status code
 code | description
---|---
100|Successfully created order
101|The required parameter has a null value
102|The format of the required parameter is incorrect
103|Duplicate purchase order number
104|SKU quantity is 0

## Request example
### parameter

```json
{
    "poNumber":"GZBL01242421",
    "remark":"test",
    "trackingBarCode":"542412421421",
    "orderId":"P2020081300001",
    "arrivalDate":"2020-08-18",
    "skudetails":[
        {
            "sku":"A0001",
            "count":1,
        },
        {
            "sku":"A0002",
            "count":2,
        }
    ]
}
```

# response
```json
{
   "code":100,
   "message":"创建成功。"
}

```



