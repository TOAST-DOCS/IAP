<!-- pre-align:aligned sig=1b5027353732 -->

<a id="mobile-service-iap-server-api-guide"></a>
## Mobile Service > IAP > Server API Guide { #mobile-service-iap-server-api-guide }

> [Notice]
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).
> No new features will be developed for the existing IAP SDK.
> This document is the guide for [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).

IAP supports server api for in app purchase.<br>





<a id="consume-api"></a>
## Consume API { #consume-api }

User Application Server should notify IAP server to consume payment before issuing item <br/>. Only one consuming is available for each payment, and if the payment is invalid, consuming will not take place. <br/>Unconsumed payment can be inquired with unconsumed payment history inquiry API of the relevant SDK.

> [Reference]  
> One consuming is available for each payment, and unconsumed payment will be considered not to have provided an item.    
> Client may inquire all unconsumed payment.

<a id="request"></a>
### Request { #request }

<a id="request-http-request"></a>
#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/consume
```

<a id="request-http-request-header"></a>
#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |


<a id="request-body"></a>
#### Request Body

| Name         | Data Type    | Description  |
| ------------- | ------ | --------------- |
| paymentSeq | String | payment unique identifier  |
| accessToken | String | API access token |


<a id="response"></a>
### Response { #response }

returns a result in the response body.

<a id="response-success"></a>
#### Success

```json
{
   "header":{
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result":{
        "price": 1500,
        "currency": "KRW",
        "productSeq": 12345
    }
}
```

<a id="response-error"></a>
#### Error
```json
{
    "header":{
        "isSuccessful": false,
        "resultCode": 5018,
        "resultMessage": "error message"
    }
}
```


<a id="response-header"></a>
#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  0 or error code |
| resultMessage |  String |  "SUCCESS" or errer message|

<a id="response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | Float   | price |
| currency      | String | currency |
| productSeq      | long | item unique identifier in IAP web console |



<a id="error-code"></a>
### Error Code { #error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 5000 | CONSUME FAILED (eg , invalid parameter, invalid status) |
| 5018 |  ALREADY CONSUMED|
| 9999 |  UNKNOWN ERROR|



<a id="consumable-list-api"></a>
## Consumable List API { #consumable-list-api }

Unconsumed payment history with payment complete status can be inquired with Server API. <br> 
You can inquire unconsumed items with the API and perform consume process.



<a id="consumable-list-api-request"></a>
### Request { #consumable-list-api-request }
<a id="consumable-list-api-request-http-request"></a>
#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/consumable
```

<a id="consumable-list-api-request-http-request-header"></a>
#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |

<a id="consumable-list-api-request-request-body"></a>
#### Request Body

| Property name | Value  | Description       |
| ------------- | ------ | --------------- |
| marketId | String | Store CODE (GG : Google, AS : Apple, ONESTORE : 원스토어) |
| userChannel | String | User Channel (GF) |
| userKey | String | User ID which you regsitered. |




<a id="consumable-list-api-response"></a>
### Response { #consumable-list-api-response }
returns a result in the response body.



<a id="consumable-list-api-response-success"></a>
#### Success

```json
{
    "header":{
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "result":[
        {
        "paymentSeq": "2016122110023124",
        "productSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "accessToken": "oJgM1EfDRjnQY7yqhWCUVgAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        },
 
        {
        "paymentSeq": "2016122110023125",
        "productSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "accessToken": "7_3zXyNJub0FNLed3m9XRAAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        }
    ]
}

```

<a id="consumable-list-api-response-header"></a>
#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  0 or error code |
| resultMessage |  String |  "SUCCESS" or errer message|


<a id="consumable-list-api-response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| paymentSeq      | String | unique payment identifier in IAP web console |
| price         | Float   | price |
| currency      | String | currency |
| productSeq      | long | item unique identifier in IAP web console |
| accessToken      | String | API access token |



<a id="consumable-list-api-error-code"></a>
### Error Code { #consumable-list-api-error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|



<a id="activesubscription-list-api"></a>
## ActiveSubscription List API { #activesubscription-list-api }
returns not expired subscription list by app and user.


<a id="activesubscription-list-api-request"></a>
### Request { #activesubscription-list-api-request }
<a id="activesubscription-list-api-request-http-request"></a>
#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/activeSubscriptionList
```

<a id="activesubscription-list-api-request-http-request-header"></a>
#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |  


<a id="activesubscription-list-api-request-request-body"></a>
#### Request Body

| Property name | Value  | Description       |
| ------------- | ------ | --------------- |
| marketId | String | Store Code (GG : Google, AS : Apple, ONESTORE : 원스토어) |
| packageName | String | App package name (eg: com.nhnent.iap.google.sample) |
| userChannel | String | user channel (GF) |
| userKey | String | User ID which you regsitered. |




<a id="activesubscription-list-api-response"></a>
### Response { #activesubscription-list-api-response }
returns a result in the response body.



<a id="activesubscription-list-api-response-success"></a>
#### Success

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "result": [
    {
      "channel": "GF",
      "userId": "default_testUserx",
      "paymentSeq": "2018102610330423",
      "appId": "com.nhnent.iap.google.sample",
      "productId": "subs_p1w",
      "productType": "AUTO_RENEWABLE",
      "productSeq": 1002904,
      "currency": "KRW",
      "price": 1000,
      "paymentId": "GPA.3375-2193-1175-57698",
      "originalPaymentId": "GPA.3375-2193-1175-57698",
      "purchaseTimeMillis": 1540522998289,
      "expiryTimeMillis": 1541134994548,
      "renewTimeMillis": 1540523045377,
      "productSeq" : 1000009
    }
  ]
}
```



<a id="activesubscription-list-api-response-error"></a>
#### Error
```json
{
    "header":{
        "isSuccessful": false,
        "resultCode": 1100,
        "resultMessage": "error message"
    }
}
```

<a id="activesubscription-list-api-response-header"></a>
#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  0 or error code |
| resultMessage |  String |  "SUCCESS" or errer message|

<a id="activesubscription-list-api-response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| channel      | String | user channel (GF) |
| userId      | String | User ID which you regsitered. |
| paymentSeq      | String | unique payment identifier in IAP web console |
| appId      | String | app package name |
| productId         | String   | product identifier in store console |
| productType      | String | consumable or auto renewable |
| productSeq      | long | item unique identifier in IAP web console|
| currency      | String | currency |
| price      | Float | price |
| paymentId      | String | latest store payment unique identifier|
| originalPaymentId      | String | original store payment unique identifier |
| purchaseTimeMillis      | long | latest renewal time in millis |
| expiryTimeMillis      | long | expiry time in millis |
| renewTimeMillis      | long | renewal enrollment or renewal notification time in millis |




<a id="activesubscription-list-api-error-code"></a>
### Error Code { #activesubscription-list-api-error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|