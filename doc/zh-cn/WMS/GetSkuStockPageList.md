## 全量分页查询产品sku库存信息接口 (未实现)
请求方式 | 请求路径
---|---
GET | /stock/getPageList

**接口说明**
*  全量查询全量产品sku库存信息接口

## 请求header说明
需增加授权token头部信息

# 参数说明
参数 | 类型 |是否必填|默认值| 说明
---|---|---|---|---
pageIndex|int|是|1|页码，从1开始
pageSize|int|是|20|分页大小(最大200条)

#  公共输出参数
参数 | 类型|描述
---|---|---
message|string|请求返回说明
code|string|请求返回状态码
data|Array| 请求返回数据集合

# items输出参数说明
字段 | 类型 |描述
---|---|---
sku|string|产品Sku编码
title|string | 中文标题
enTitle|string|英文标题
pendingStock|long|货物已在途待上架库存数量(供应商已经发货，货物在途中，还没有到达仓库的数量)
availabelStock|long|产品sku可发货库存数量(仓库内真实的可以发货的库存数量)
shippedStock|long|产品sku已发货库存数量(仓库实际已经发出去的库存数)
lastModificationTime|datetime|产品sku库存最后变动时间(UTC)

# pages 输出参数说明
字段 | 类型 |描述
---|---|---
total|int|数据总条数
currentPage|int|当前页
pageSize|int|分页大小

# 请求示例
```
curl -X GET url + '/stock/getPageList?pageSize=10&pageIndex=1
```

# 响应示例
```
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
# 错误示例
```
{
	"message": "必填项参数有空值",
	"code": 101
}
```

## 请求返回的状态码code的说明
 code | 说明
---|---
100|查询产品sku库存信息成功
101|必填项参数有空值
102|必填项参数格式不对
