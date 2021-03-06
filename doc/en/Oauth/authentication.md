## Third-party application obtains access token
Generate access token, to access resource service API

Request method | Request path
---|---
POST | /oauth/token/get

**Api Call instructions**
* Before calling, please configure the third-party application information in the OAuth service. The authorization center will provide the appId and app key.
* Please note that the authorization token has an expiration time limit. If you use the Token to access the protected resource API and return a 401 status code, you need to call this interface again to obtain a new authorization token.

# Parameter Description
## Input parameters
parameter | type | Is required  | Field description  
---|---|---|---
app_id | String | True | Provided third-party application appid
app_key | String | True | Provided third-party application key

## Output parameters
parameter | type | Example data | Field description  | 
---|---|---|---
app_id | String | S12345945 | Provided third-party application appid | 
access_token | String | Bearer eyJ...e6mCRQ | access token
expires_in | Integer | 3600 | Token validity period
status_code | Integer | 200 | status code
err_msg | String | Illegal id |Prompt message when an error occurs 

Common status codes: normal (200), error request (400), service error (500), unauthorized (401), access forbidden (403).

## Access process
![avatar](https://eumengman.blsct.com/Oauth%E6%B5%81%E7%A8%8B.png)

## Test Case
* Authorized service url：https://coupang.blsct.com/oauth/token/get
* Test resource Api：
  
Request url | Request method | Authorization required |
---|---|---|
https://testapi.coupang.blsct.com/test | GET |No |
https://testapi.coupang.blsct.com/test/get?id=1 | GET | Yes |

Authorization-request
```
https://coupang.blsct.com/oauth/token/get
POST application/json
{
    "app_id":"your appId",
    "app_secret":"your appSecret"
}
```
Authorization-response
```
{
    "appId": "100635296",
    "accessToken": "Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkJBREM3QTNCQ0U5RjlFQUNFNDg1RjI4NkU5QzU1ODM5OUJCMkM4MUNSUzI1NiIsInR5cCI6ImF0K2p3dCIsIng1dCI6InV0eDZPODZmbnF6a2hmS0c2Y1ZZT1p1eXlCdyJ9.eyJuYmYiOjE1OTc3MTczNTAsImV4cCI6MTU5NzcyMDk1MCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDA2IiwiY2xpZW50X2lkIjoiMTAwNjM1Mjk2IiwianRpIjoiOUQ0RTNFNDczQTI5MEU1MjAxRUMwMTUyRTNCN0FBRTciLCJpYXQiOjE1OTc3MTczNTAsInNjb3BlIjpbImJhaWx1bkFwaSJdfQ.mZiueNr1MjaKNK3UaXTTPYLMd87VLREj9Wi1uKQcRJ914FM74phhM9U0NrPpQ5xry1nFCQL4hMsZ7hU9O0Z9-NcGqk6oKKIAItUAONVdeRMhuVYZ1RKxZEj77y8oyXmSvTYSRman7P3RJeDWkWe-vdT7kLySxdWjwqtiRczJhqZA2gxfBCwLmqMyON_N4jCuj2N49765E1l2kq4aFmAdgq7ED8bYH0l7M4MfxOU-I4i5bEFB-h3A4I1S0NJABBj4Mw6vzSjPuQkQ1asMdM_I7BzHj82CrpLN15ExLalgTvBGqqt79de4cfrJa4S96NY3-DPUzLAg",
    "expiresIn": 3600,
    "statusCode": 200,
    "errMsg": null
}
```
Resource api-request
```
https://testapi.coupang.blsct.com/product/get?id=1
Get 
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkJBREM3QTNCQ0U5RjlFQUNFNDg1RjI4NkU5QzU1ODM5OUJCMkM4MUNSUzI1NiIsInR5cCI6ImF0K2p3dCIsIng1dCI6InV0eDZPODZmbnF6a2hmS0c2Y1ZZT1p1eXlCdyJ9.eyJuYmYiOjE1OTc3MTQ0NTAsImV4cCI6MTU5NzcxODA1MCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo1MDA2IiwiY2xpZW50X2lkIjoidGVzdENsaWVudCIsImp0aSI6IjYyNDMwRDM4QjFGMzI4NEI4Q0NGODFCRDdEMUVCNkI0IiwiaWF0IjoxNTk3NzE0NDUwLCJzY29wZSI6WyJiYWlsdW5BcGkiXX0.YlhbfO7bTcSiO2kJ5aBOURZn4DWxN-ZGp-niKrw3zOtPSE7BfqAo1opjTyTqIE_MbXQCobYHP2XUvNhaV8kfArOsD-Ip75NXlxEx9XcedgEARJ9yCXFVW6T_U-0LSdm6dgYsTlXypc_Ut9uyEWUJL35dglfRPDb16y6EdPg8YZvyRYAhARZLPhkGLAvruipjT74fnuO-AIYS02KoYCaChnUsoOFIL4r11nX8gsLUkMuHqwqjngFVjjMJSd1QL9iluTv5_sqYAsOKcvS2aS4OVf-VnGqeE7Revn7BEGjQ1GkIQBJ0onBFHg5b5rf9Ulasw
```
Resource api-response(Authorized)
```
Ok!You successfully caught me. The Id is 1
```
Resource api-response(No Authorized)
```
401
```
