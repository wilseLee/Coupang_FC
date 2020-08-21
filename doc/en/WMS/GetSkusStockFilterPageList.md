## Incremental query product sku inventory information (Not implemented)
Request method | Request path
---|---
GET | /stock/getFilterPageList

**Interface Description**
*  Incremental paging query product sku inventory information
*  You can filter and query according to the sku code and the last product sku inventory change time

## Request header description
Need to add authorization token header information

# Input parameter description
Parameter | Type | Required | Default value | Description
---|---|---|---|---
pageIndex|int|true|1|Page number, starting from 1
pageSize|int|true|20|Page capacity (maximum 200)
sku|string|false||Single product sku code
startDate|datetime|true||Incremental query start time(UTC)
endDate|datetime|true||Incremental query end time(UTC)

#  Common output parameters
Parameters | Type | Description
---|---|---
message|string|Request return information
code|string|Request return status code
data|Array| Request to return data collection

# Output parameter description
### items DTO
Field | Type | Description
---|---|---
sku|string|Product Sku
title|string | Chinese title
enTitle|string|English title
pendingStock|long|The goods are in transit and waiting to be put on the shelf inventory quantity
availabelStock|long|Product sku can ship inventory quantity
shippedStock|long|Product sku has shipped inventory quantity
lastModificationTime|datetime|Product sku inventory last change time(UTC)

### pages DTO
Field | Type | Description
---|---|---
total|int|Total number of data
currentPage|int|current page
pageSize|int|Paging Size
# Request example
```
curl -X GET url + '/stock/getFilterPageList?pageSize=10&pageIndex=1&sku=ND0157&startDate=2020-07-01&endDate=2020-08-01
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
```
{
	"message": "增量查询开始时间必填",
	"code": 103
}
```
# Description of response parameter status code
 code | description
---|---
100|Query product sku inventory information successfully
101|Required parameter has null value
102|The required parameter format is incorrect
103|Incremental query start time is required
104|Incremental query end time is required