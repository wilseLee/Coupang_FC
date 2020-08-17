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
