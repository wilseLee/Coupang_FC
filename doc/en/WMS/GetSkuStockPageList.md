## Full query product sku inventory information (Not implemented)
Request method | Request path
---|---
GET | /stock/getPageList

**Interface Description**
*  Full query full product sku inventory information interface

## Request header description
Need to add authorization token header information

# Parameter Description
Parameter | Type | Required | Default value | Description
---|---|---|---|---
pageIndex|int|true|1|Page number, starting from 1
pageSize|int|true|20|Paging capacity (maximum 200)

## Common output parameters
Parameters | Type | Description
---|---|---
message|string|Request return instructions
code|string|Request return status code
data|Array| Request to return data array

# items DTO
Field | Type | Description
---|---|---
sku|string|Product Sku code
title|string | Chinese title
enTitle|string|English title
pendingStock|long|The goods are in transit and waiting to be put on the shelf inventory quantity(The supplier has shipped the goods, the goods are on the way, and the quantity has not reached the warehouse)
availabelStock|long|Product sku can ship inventory quantity(The actual inventory quantity that can be shipped in the warehouse)
shippedStock|long|Product sku shipped inventory quantity(The actual number of stocks that the warehouse has sent out)
lastModificationTime|datetime|The last change time of product sku inventory(UTC)

# pages DTO
Field | Type | Description
---|---|---
total|int|Total number of data
currentPage|int|current page number
pageSize|int|Paging Size

# Request example
```
curl -X GET url + '/stock/getPageList?pageSize=10&pageIndex=1
```

# Response example
```json
{
	"message": "",
	"code": 100,
	"data": {
		"items": [{
			"sku": "ND0157",
			"title": "",
			"enTitle": "",
			"pendingStock": 0,
			"availabelStock": 1012,
			"shippedStock": 5,
			"lastModificationTime": "2019-07-06T16:32:17.64875"
		}],
		"pages": {
			"total": 1,
			"currentPage": 1,
			"pageSize": 20
		}
	}
}
```
# Error example
```json
{
	"message": "必填项参数有空值",
	"code": 101
}
```

## Description of response parameter status code
 code | description
---|---
100|Query product sku inventory information successfully
101|Required parameter has null value
102|The required parameter format is incorrect
