<!-- pre-align:aligned sig=b412443601e5 -->

<a id="common-iap-server-developers-guide"></a>
## Common > IAP > Server Developer's Guide { #common-iap-server-developers-guide }

<a id="payment-consume-api"></a>
## Payment Consume API { #payment-consume-api }

User Application Server should notify IAP server to consume payment before issuing item <br/>. Only one consuming is available for each payment, and if the payment is invalid, consuming will not take place. <br/>Unconsumed payment can be inquired with unconsumed payment history inquiry API of the relevant SDK.

> [Reference]  
> One consuming is available for each payment, and unconsumed payment will be considered not to have provided an item.    
> Client may inquire all unconsumed payment.

<a id="request"></a>
### Request { #request }

[URL]

```http
POST https://api-iap.cloud.toast.com/inapp/v3/consume/{paymentSeq}/items/{itemSeq}
```

[Request Header]

| Property name | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |

[Path Parameter]

| Name         | Data Type    | Description                     |
| ---------- | ------ | ---------------------- |
| paymentSeq | String | payment unique identifier                 |
| itemSeq    | Long   | item unique identifier obtained in web console |

[RequestBody]

| Name         | Data Type    | Description                     |
| ------------- | ------ | --------------- |
| purchaseToken | String | token for payment verification |

[Example]

```http
POST https://api-iap.cloud.toast.com/inapp/v3/consume/2014090210002254/items/1032032

RequestBody
{
	"purchaseToken":"5PYSHgisiCU8BditHnDbPhmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA=="
}
```

<a id="response"></a>
### Response { #response }


[Example Response]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "request is successful",
        "isSuccessful": true
    },
    "result": {
        "price":1000.0,
        "currency":"KRW"
    }
}
```

[Header]

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | consume is successful or not.(true/false)
| resultCode |  Integer |  detail code when consume fails.|
| resultMessage |  String |  detail message |

[Result]

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | long   | price |
| currency      | String | currency |

[ResultCode]

| Value | Description             |
| - | -------------- |
| 0 | 0 when consume is successful. |

> [Reference]  
> other Result Code    
> Refer to Error Code page.  

<br/>
> [Reference]  
> Even though the existing consume API v2 can be called, it will soon become unavailable. 


<a id="payment-consumable-api"></a>
## Payment Consumable API { #payment-consumable-api }

Unconsumed payment history with payment complete status can be inquired with Server API. <br/> You can inquire unconsumed items with the API and perform consume process.

<a id="payment-consumable-api-request"></a>
### Request { #payment-consumable-api-request }

[URL]

```http
POST https://api-iap.cloud.toast.com/standard/inapp/v1/consumable/list
```

[Request Header]

| Property name | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |


[RequestBody]

| Name            | Data Type    | Description              |
| ------------- | ------ | --------------- |
| appSeq | Long | app unique identifier obtained in web console |
| userChannel | String | user channel <br/>(default value : "GF") |
| userKey | String | user identifier |

[Example]

```http
POST https://api-iap.cloud.toast.com/standard/inapp/v1/consumable/list

RequestBody
{
  "appSeq" : "1000272",
  "userChannel" : "GF",
  "userKey" : "tester"
}
```

<a id="payment-consumable-api-response"></a>
### Response { #payment-consumable-api-response }


[Example Response]

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
        "itemSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "purchaseToken": "oJgM1EfDRjnQY7yqhWCUVgAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        },
 
        {
        "paymentSeq": "2016122110023125",
        "itemSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "purchaseToken": "7_3zXyNJub0FNLed3m9XRAAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        }
    ]
}

```

[Header]

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | inquiry is successful (true/false)|
| resultCode |  Integer |  detail code when inquiry fails. |
| resultMessage |  String |  detail message |

[Result]

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| paymentSeq |  String | payment unique identifier(PAYMENT ID) |
| itemSeq |  String |  ITEM ID obtained in web console |
| currency | Long |  currency |
| price |  String |  price |
| purchaseToken |  String | token for payment verification and consume |

[ResultCode]

| Value | Description             |
| - | -------------- |
| 0 |  successful payment count, not yet consumed|

> [Reference]  
> other Result Code    
> Refer to Error Code page.  


<a id="item-search-api"></a>
## Item Search API { #item-search-api }

Inquire items registered to App ID in web console.

<a id="item-search-api-request"></a>
### Request { #item-search-api-request }

[URL]

```http
POST https://api-iap.cloud.toast.com/standard/item/list/{appSeq}

```

[Request Header]

| Property name | Value            |
| ------------- | ---------------- |
| Http Method   | GET             |

[Path Parameter]

| Name         | Data Type    | Description                     |
| ---------- | ------ | ---------------------- |
| appSeq    | Long   | appSeq obtained in web console |


[Example]

```http
POST https://api-iap.cloud.toast.com/standard/item/list/1000047
```

<a id="item-search-api-response"></a>
### Response { #item-search-api-response }


[Example Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "result": {
        "appUsingStatus": "USE",
        "itemList": [
            {
                "itemSeq": 1000059,
                "itemName": "gas",
                "marketItemId": "gas",
                "usingStatus": "USE",
                "regYmdt": "2014-12-05 07:02:34",
                "appName": "Google Unity Test App",
                "marketId": "GG"
            }
        ],
        "marketAppId": "com.nhnent.rich.smuggler",
        "appSeq": "1000047"
    }
}



```

[Header]

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | inquiry is successful or not. (true/false) |
| resultCode |  Integer | detail code when inquiry fails. |
| resultMessage |  String |  detail message |

[Result]

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| appUsingStatus | String | in use : "USE" , not use : "STOP" |
| itemList | List | object list containing item |
| itemSeq | Long | item seq registered in web console|
| itemName | String | item name registered in web console|
| marketItemId | String | store item name registered in web console|
| usingStatus | String | in use : "USE" , not use : "STOP" |
| regYmdt | String | ITEM registration date |
| appName | String | app name of ITEM|
| marketId | String | store of ITEM  <br/>Google Play : "GG"<br/> Apple App Store : "AS" <br/>One Store : "TS" |
| marketAppId | String | Store App ID registered in web console |
| appSeq | Long | App ID registered in web console|

[ResultCode]

| Value | Description             |
| - | -------------- |
| 0 | 0 when inquiry is successful |

> [Reference]  
> other Result Code    
> Refer to Error Code page.  