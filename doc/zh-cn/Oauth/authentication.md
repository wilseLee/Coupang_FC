## 第三方应用获取访问Token
生成访问Token，访问资源服务API

请求方式 | 请求路径
---|---
POST | /oauth/token/get

**调用说明**
* 调用前请先在OAuth服务进行配置第三方应用信息，百伦将提供appId和app密钥。
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
