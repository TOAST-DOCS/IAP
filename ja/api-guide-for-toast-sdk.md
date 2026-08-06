<!-- pre-align:aligned sig=1b5027353732 -->

<a id="mobile-service-iap-server-api-guide"></a>
## Mobile Service > IAP > Server API ガイド { #mobile-service-iap-server-api-guide }


> [お知らせ]
> 定期購入決済をサポートする新規のIAP SDKが[NHN Cloud SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)として発売されました。
> 既存IAP SDKはこれ以上新規機能を開発しない予定です。
> 本文書は[NHN Cloud SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)ガイドです


IAPを連動するときに開発会社のサーバーで使用できるAPIです。<br>


<a id="consume-api"></a>
## Consume API { #consume-api }

ユーザアプリケーションサーバーは、アイテムを支給する前に、IAP サーバーに決済を消費することをお知らせする必要があります。 <br>
決済1件当たり1回だけ決済消費が可能で、決済の状態が正常でないと消費されません。 <br>
消費(Consume)していない決済内訳は、SDKの未消費決済内訳照会APIにて照会されます。<br>
商品タイプがCONSUMABLEの決済のみ消費が可能です。



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

| Property name | Value   | Description             |
| ------------- | ------ | --------------- |
| paymentSeq | String | 決済番号 |
| accessToken | String | API Accessのためのトークン情報 |


<a id="response"></a>
### Response { #response }

Response bodyにJSON形に配信

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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

<a id="response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | Float   | price |
| currency      | String | currency |
| productSeq      | long | 決済のアイテム番号 (consoleに登録されたアイテム固有番号) |



<a id="error-code"></a>
### Error Code { #error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 5000 | CONSUME FAILED (例:パラメータ誤りなど) |
| 5018 |  ALREADY CONSUMED|
| 9999 |  UNKNOWN ERROR|



<a id="consumable-list-api"></a>
## Consumable List API { #consumable-list-api }

決済が完了しましたが、消費(consume)されていない決済内訳をServer APIで照会することができます。 <br>


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
| marketId | String | ストアコード (GG : Google, AS : Apple) |
| userChannel | String | ユーザーチャンネル (GF) |
| userKey | String | ユーザ識別キー |




<a id="consumable-list-api-response"></a>
### Response { #consumable-list-api-response }
Response bodyにJSON形に配信



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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

<a id="consumable-list-api-response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| paymentSeq      | String | 決済番号 |
| productSeq      | long | 決済のアイテム番号 (コンソールに登録されたアイテム固有番号) |
| price         | Float   | price |
| currency      | String | currency |
| accessToken      | String | API accessのためのトークン |



<a id="consumable-list-api-error-code"></a>
### Error Code { #consumable-list-api-error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|



<a id="activesubscription-list-api"></a>
## ActiveSubscription List API { #activesubscription-list-api }
アプリ別、ユーザ別に満了していない定期購入決済を照会する。


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

| Property name | Value   | Description             |
| ------------- | ------ | --------------- |
| marketId | String | ストアコード (GG : Google, AS : Apple) |
| packageName | String | APP packageName (例: com.nhnent.iap.google.sample) |
| userChannel | String | ユーザーチャンネル (GF) |
| userKey | String | ユーザ識別キー |



<a id="activesubscription-list-api-response"></a>
### Response { #activesubscription-list-api-response }
Response bodyにJSON形に配信



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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

<a id="activesubscription-list-api-response-result"></a>
#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| channel      | String | ユーザーチャンネル (GF) |
| userId      | String | ユーザ識別キー |
| paymentSeq      | String | 決済番号 |
| appId      | String | packageName |
| productId         | String   | ストアーに登録された商品識別子 |
| productType      | String | 商品タイプ |
| productSeq      | long | 決済のアイテム番号 (コンソールに登録されたアイテム固有番号)|
| currency      | String | currency |
| price      | Float | price |
| paymentId      | String | 最近更新されたストアの決済番号 |
| originalPaymentId      | String | 最初のストア決済番号 |
| purchaseTimeMillis      | long | 最近更新された時間 |
| expiryTimeMillis      | long | 満了時間 |
| renewTimeMillis      | long | 更新登録または更新通知発生時間     |




<a id="activesubscription-list-api-error-code"></a>
### Error Code { #activesubscription-list-api-error-code }

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|
