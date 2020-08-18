## 第三方应用获取访问Token
生成访问Token，访问资源服务API

请求方式 | 请求路径
---|---
POST | /oauth/token/get

**调用说明**
* 调用前请先在OAuth服务进行配置第三方应用信息，授权中心将提供appId和app密钥。
* 请注意授权Token有过期时间限制，若使用Token访问受保护的资源Api返回401状态码时，需重新调用此接口获取新的授权Token。

# 参数说明
## 输入参数
参数 | 类型 | 是否必填  | 字段说明  
---|---|---|---
app_id | String | True | 提供的第三方应用id
app_key | String | True | 提供的第三方应用密钥

## 输出参数
参数 | 类型 | 示例 | 字段说明 | 
---|---|---|---
app_id | String | S12345945 | 内部应用id | 
access_token | String | Bearer eyJ...e6mCRQ | 颁发的令牌Token
expires_in | Integer | 3600 | 令牌Token有效期时长
status_code | Integer | 200 | 状态码
err_msg | String | 非法id |发生错误时提示信息 

常用状态码：正常(200)、错误请求(400)、服务错误(500)、未授权(401)、禁止访问(403)

## 访问流程
![avatar](https://eumengman.blsct.com/Oauth%E6%B5%81%E7%A8%8B.png)

## 测试用例
* 授权服务地址：https://coupang.blsct.com/oauth/token/get
* 测试资源Api地址：
  
请求地址 | 请求方式 |需要授权 |
---|---|---|
http://testapi.coupang.blsct.com/product | GET |不需要|
http://testapi.coupang.blsct.com/product/get?id=1 | GET |需要 |

授权-请求
```
https://coupang.blsct.com/oauth/token/get
POST applocation/json
{
    "app_id":"coupang",
    "app_secret":"coupangTest"
}
```
授权-返回
```
{
    "appId": "coupang",
    "accessToken": "Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkJBREM3QTNCQ0U5RjlFQUNFNDg1RjI4NkU5QzU1ODM5OUJCMkM4MUNSUzI1NiIsInR5cCI6ImF0K2p3dCIsIng1dCI6InV0eDZPODZmbnF6a2hmS0c2Y1ZZT1p1eXlCdyJ9.eyJuYmYiOjE1OTc3MTUwNDQsImV4cCI6MTU5NzcxODY0NCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDA2IiwiY2xpZW50X2lkIjoiY291cGFuZyIsImp0aSI6IjQwNTg1NzQ0RTQ5NTNCRDYxMkFCOTg4RTZBQTNGRTg5IiwiaWF0IjoxNTk3NzE1MDQ0LCJzY29wZSI6WyJiYWlsdW5BcGkiXX0.PoMdVpRpNdVo4Ug7ogiexyPMJZ3bsV3jyZtSEdJUXg8OTRaW3Ly_HKg_7DqqyzAhnOT7FZ6XSRG0HBKii16PjTxub62jJWZlvcEo2GdZtSoU74rJ3-l-D3y4c0bKkpRotgZBUW77OJhBkzAcli2rj3xbKhUxeDHn-81rWj-Gc34UgO_Uk3UHLqGm1Ol5b_BGuT3HHPQZtKWuf3zl_d4l1SS05kXce-8i2dvU8nKfIsjs5sbODcJAMYj1YpvUEiLgo7b_uVMo1EQ-75r2cf64d_V7LGnDgcdBsWEtzDQlap4KPGJNGDExQwDKJ50QNRrHlqPqYQC7rA5FXvnDdZYz-w",
    "expiresIn": 3600,
    "statusCode": 200,
    "errMsg": null
}
```
请求资源-请求
```
http://testapi.coupang.blsct.com/product/get?id=1
Get 
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkJBREM3QTNCQ0U5RjlFQUNFNDg1RjI4NkU5QzU1ODM5OUJCMkM4MUNSUzI1NiIsInR5cCI6ImF0K2p3dCIsIng1dCI6InV0eDZPODZmbnF6a2hmS0c2Y1ZZT1p1eXlCdyJ9.eyJuYmYiOjE1OTc3MTQ0NTAsImV4cCI6MTU5NzcxODA1MCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDA2IiwiY2xpZW50X2lkIjoidGVzdENsaWVudCIsImp0aSI6IjYyNDMwRDM4QjFGMzI4NEI4Q0NGODFCRDdEMUVCNkI0IiwiaWF0IjoxNTk3NzE0NDUwLCJzY29wZSI6WyJiYWlsdW5BcGkiXX0.YlhbfO7bTcSiO2kJ5aBOURZn4DWxN-ZGp-niKrw3zOtPSE7BfqAo1opjTyTqIE_MbXQCobYHP2XUvNhaV8kfArOsD-Ip75NXlxEx9XcedgEARJ9yCXFVW6T_U-0LSdm6dgYsTlXypc_Ut9uyEWUJL35dglfRPDb16y6EdPg8YZvyRYAhARZLPhkGLAvruipjT74fnuO-AIYS02KoYCaChnUsoOFIL4r11nX8gsLUkMuHqwqjnMgCI4ihlefkhqCY0sP9m-gFVjjMJSd1QL9iluTv5_sqYAsOKcvS2aS4OVf-VnGqeE7Revn7BEGjQ1GkIQBJ0onBFHg5b5rf9Ulasw
```
请求资源-返回(有授权)
```
Ok!You successfully caught me. The Id is 1
```
请求资源-返回(无授权)
```
401
```


