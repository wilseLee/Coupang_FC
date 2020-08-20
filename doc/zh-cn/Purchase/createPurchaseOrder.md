## 采购下单
请求方式 | 请求路径
---|---
|Post | /api/purchase/service/createPurchaseOrder

## 请求header说明
需增加token头部信息，token来自oauth授权服务

# 输入参数说明
## 输入参数
字段 | 类型 | 是否必填 | 说明
---|---|---|---
poNumber|string|是|采购单号
trackingBarCode|string|是|物流跟踪条码(用于线下扫码）
remark|string|否|下单备注
orderId|string|是|订单号
arrivalDate|date|是|预计到货送达仓库的日期
skudetails|List&lt;skudetail&gt;|是|sku明细




## skudetail字段说明
字段 | 类型 | 是否必填 | 说明
---|---|---|---
sku|string|是|sku编码 
count|int|是|sku数量



## 返回字段说明
字段 | 类型 | 说明|
---|---|---
code|int|请求返回状态码|
message|string|请求消息|


## 请求返回的状态码code的说明
 code | 说明
---|---
100|创建订单成功
101|必填项参数有空值
102|必填项参数格式不对
103|采购单号重复
104|SKU数量为0


## 请求示例

```
# 请求
POST /api/purchase/service/createPurchaseOrder

# 参数
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

# 返回
{
   "code":100,
   "message":"创建成功。"
}

```



