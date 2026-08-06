<!-- machine_translated: true -->

<a id="mobile-service-iap-android-sdk-guide"></a>

## Mobile Service > IAP > Android SDK Guide { #mobile-service-iap-android-sdk-guide }


> [Notice]
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/en/TOAST/ko/toast-sdk/overview/).
> No new features will be developed for the existing IAP SDK.


<a id="development-environment"></a>

## Development Environment { #development-environment }
* Android Studio IDE 2.3.3 or later
* Android SDK Version is beyond **2.3.3 (API Level 10)**

The open sources in use are as follows.

|Name|Reference|Version|License|
|---|---|---|---|
|okhttp|http://square.github.io/okhttp/|1.5.4|Apache License 2.0|
|gson|https://code.google.com/p/google-gson/|2.2.4|Apache License 2.0|

<a id="using-in-android-studio-gradle"></a>

## Using in Android Studio & Gradle { #using-in-android-studio-gradle }

`NHN Cloud IAP SDK` offers development environment for Gradle-based Android Studio IDE.
Remote downloading is available from jCenter Maven Repository.
Define repository and dependency in build.gradle file of the project as below.

<a id="gradle-repository"></a>
### 1. Gradle Repository { #gradle-repository }

```
buildscript {
    repositories {
        jcenter()
    }
}
```

The common permissions used by `NHN Cloud IAP SDK` are as follows.

|Permission|Description|
|---|---|
|android.permission.INTERNET|Allows the application to open network sockets.|
|com.android.vending.BILLING|Grants the application in-app purchase permission.|

<br/>

<a id="adding-dependencies"></a>
### 2. Adding Dependencies { #adding-dependencies }
<a id="adding-dependencies-google-play-store"></a>
#### Google Play Store
```
dependencies {
    implementation 'com.toast.iap:iap:1.5.0'
}
```
<a id="adding-dependencies-sdk-v17-api-v5---recommended"></a>
#### SDK v17 (API v5) - Recommended
```
dependencies {
    implementation 'com.toast.iap:iap-onestore:1.5.0'
}
```
The added permissions are as follows.

|Permission|Description|
|---|---|
|android.permission.ACCESS_NETWORK_STATE|Allows the application to access information about networks.|

<a id="adding-dependencies-sdk-v16-api-v4"></a>
#### SDK v16 (API v4)
```
dependencies {
    implementation 'com.toast.iap:iap-tstore:1.5.0'
}
```

<br/>

> [Note]  
> Release History   
> Please refer to RELEASE-NOTES.md within package for SDK version history.

<a id="one-store-configuration-information"></a>

## One Store Configuration Information { #one-store-configuration-information }

Starting Tuesday, June 12, 2018, new apps using the legacy SDK v16 (API v4) or earlier can no longer be registered.
If you are working on a new app, use SDK v17 (API v5).

* [Notice of end of support for products using In-App SDK versions below v15.xx.xx](https://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?page.no=1&orderValue=&orderType=&noticeId=31245&noticeNo=789&pageFlag=List&searchValue=)
* [Notice of inability to register new apps using the legacy IAP SDK](https://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?page.no=1&orderValue=&orderType=&noticeId=31224&noticeNo=788&pageFlag=List&searchValue=)

<a id="sdk-v17-api-v5"></a>
### 1. SDK v17 (API v5) { #sdk-v17-api-v5 }

<a id="sdk-v17-api-v5-promoting-one-store-update-and-installation"></a>
#### Promoting One Store Update and Installation

If the SDK error code `INAPP_ONESTORE_NEED_UPDATE(201)` occurs, you can prompt installation by using the following code.
```java
Intent intent = new Intent("android.intent.action.VIEW");
intent.setData(Uri.parse("http://m.onestore.co.kr/mobilepoc/etc/downloadGuide.omp"));
startActivity(intent);
```

<a id="sdk-v17-api-v5-requesting-one-store-login"></a>
#### Requesting One Store Login

The `NHN Cloud IAP SDK` checks the login status internally, so you do not need to handle login separately.
If the user is not logged in during use, a One Store login popup (Yes/No) will appear.
If you select `Yes` in the login popup, you will be directed to the One Store login screen. If you select `No`, an `INAPP_ONESTORE_NEED_LOGIN(202)` error is raised.

> [Note]  
> [Requesting One Store Login](https://dev.onestore.co.kr/devpoc/reference/view/IAP_v17_05_implementation#HC6D0C2A4D1A0C5B4B85CADF8C778C694CCADD558AE30-getLoginIntent2829)

<a id="sdk-v17-api-v5-using-popup-payment-screen"></a>
#### Using Popup Payment Screen

If you want to use the popup-style payment screen, add the following settings to `AndroidMenifest.xml`.
```xml
<application>
    <meta-data 
        android:name="iap:view_option" 
        android:value="popup | full" />
</application>
```

> [Note]  
> [OneStore - Prerequisites for applying in-app purchase > 7. Android Manifest file settings](https://dev.onestore.co.kr/devpoc/reference/view/IAP_v17_04_preparation#HAndroidManifestD30CC77CC124C815)

<a id="sdk-v16-api-v4"></a>
### 2. SDK v16 (API v4) { #sdk-v16-api-v4 }

For payment testing, add the following settings to `AndroidMenifest.xml`.
```
<application>
    <meta-data 
        android:name="iap:plugin_mode" 
        android:value="development" />
</application>
```

<a id="implementing-sample-application"></a>

## Implementing Sample Application { #implementing-sample-application }

IAP Android SDK provides sample applications for Google Play Store and One Store.
You can use the sample applications to easily test the features provided by IAP Android SDK.

> [Note]  
> Notes before testing  
> Before testing payments, read the [Console User Guide](/Mobile Service/IAP/en/console-guide/) and complete the console environment setup first.

<a id="import-project"></a>
### 1. Import Project { #import-project }

Import the `/sample` directory from the distributed SDK package into Android Studio using **Import Project**.

<a id="setting-market-information-to-androidmanifestxml"></a>
### 2. Setting Market Information to AndroidManifest.xml { #setting-market-information-to-androidmanifestxml }

Set the `Store APP ID` registered in the IAP Web Console to match the applicationId of the sample application.
```
android {
    defaultConfig {
        applicationId "your app id"
    }
}
```

> [Note]  
> applicationId  
> This must match the information of the actual store (Google Play Store, One Store).

<a id="android-reference"></a>

## API Reference { #android-reference }
<a id="activating-log-information"></a>
### 1. Activating Log Information { #activating-log-information }
Activates the exposure of log information for debugging.

**[Method]**
```java
public void setDebugMode(boolean isDebuggable);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Boolean | isDebuggable | Whether to expose debugging logs |

**[Example Code]**  

```java
InAppPurchases.InAppPurchase.setDebugMode(true);
```

<br/>

<a id="store-market-settings"></a>
### 2. Store (Market) Settings { #store-market-settings }
Sets the store (market) to use during SDK initialization.

**[Market ID by Store]**

|MarketId|Store|  
|---|---|  
|GG|Google Play Store|  
|TS|One Store SDK V16 (API V4) - formerly TStore|  
|ONESTORE|One Store SDK V17 (API V5)|  

**[Method]**

```java
public boolean registerMarketId(String marketId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| String | marketId | Market ID |

**[Example Code]**  

When configured in `AndroidMenifest.xml`:
```xml
<meta-data 
    android:name="com.toast.iap.config.market" 
    android:value="GG" />
```
When configured in `Java` code:
```java
InAppPurchases.InAppPurchase.registerMarketId(marketId); // marketId : String value
```

<br/>

<a id="registering-app-id"></a>
### 3. Registering App ID { #registering-app-id }
The service ID required to use the IAP Android SDK.
The App ID can be found in `NHN Cloud Console > Mobile Service > IAP`.

**[Method]**

```java
public boolean registerAppId(long appId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Long | appId | App ID issued from the IAP Service in the NHN Cloud console |

**[Example Code]**  

When configured in `AndroidMenifest.xml`:
```xml
<meta-data 
    android:name="com.toast.iap.config.appId" 
    android:value="1234567" />
```
When configured in `Java` code:
```java
InAppPurchases.InAppPurchase.registerAppId(1234567);// appId : long integer
```
<br/>

<a id="registering-user-identifier"></a>
### 4. Registering User Identifier { #registering-user-identifier }

Registers the user ID of an authenticated user.  
This is the user identifier defined by the developer, and is the target to whom items are granted.

**[Method]**

```java
public boolean registerUserId(String userId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| String | userId | User ID identifier |

**[Example Code]**  

```java
InAppPurchases.InAppPurchase.registerUserId(userId); // userId : String value
```

<br/>

<a id="request-payment"></a>
### 5. Request Payment { #request-payment }

Requests item purchase from the client.
The response to the payment request is delivered via PurchaseCallback.
Once payment is successfully completed, send the result to the server to proceed with [9. Payment Consumption](/Mobile%20Service/IAP/en/android-sdk-guide/#9).

> [Note]  
> In-App Purchase is proceeded in two stages: payment request and payment consumption.  
> [IAP Payment Flow](/Mobile%20Service/IAP/en/Overview/#iap)  

**[Method]**
```java
public void requestPurchase(Activity activity, long itemId, PurchaseCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | Current activity of the application |
| Long | itemId | Item ID issued from the Web Console |
| PurchaseCallback | callback | Callback that returns the API request result |

**[Example Code]**  
```java
InAppPurchases.InAppPurchase.requestPurchase(this, 1000001, new PurchaseCallback() {

    @Override
    public void onCallback(JSONObject result, InAppPurchaseException exception) {
           if (!result.isSuccess()) {
              // An error occurred, we need to handle the error
              return;
           }
           // Success! Include your code to handle the results here
       }
});
```

**[Response Example]**

```json
{
    "paymentSeq": "2014082210002092",
    "purchaseToken": "5PYSHgisiCU8BditHnDbPhmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA==",
    "itemSeq": 1000001,
    "currency": "KRW",
    "price": 1000.0
}
```

<br/>

<a id="inquiry-unconsumed-user-payment-history"></a>
### 6. Inquiry Unconsumed User Payment History { #inquiry-unconsumed-user-payment-history }

Retrieves the unconsumed payment history of a user.

**[Method]**
```java
public void queryPurchases(Activity activity, PurchaseListCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | Current activity of the application |
| PurchaseCallback | callback | Callback that returns the API request result |

**[Example Code]**

```java
InAppPurchases.InAppPurchase.queryPurchases(this, new PurchaseListCallback() {

    @Override
    public void onCallback(JSONArray result, InAppPurchaseException exception) {
           if (!result.isSuccess()) {
              // An error occurred, we need to handle the error
              return;
           }
           // Success! Include your code to handle the results here }
});
```

**[Response Example]**

```json
[{
    "paymentSeq": "2014082210002092",
    "purchaseToken": "5PYSHgisiCU8BditHnDbPhmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA==",
    "itemSeq": 1000208,
    "currency": "KRW",
    "price": 1000.0
}, {
    "paymentSeq": "2014082210002093",
    "purchaseToken": "Q+os4dDsYaGiEEqkLeXQfhmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA==",
    "itemSeq": 1000208,
    "currency": "KRW",
    "price": 1000.0
}, {
    "paymentSeq": "2014082210002094",
    "purchaseToken": "GMBcODtMnX306wVlFGIcDRmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA==",
    "itemSeq": 1000208,
    "currency": "KRW",
    "price": 1000.0
}]
```

<br/>

<a id="inquiry-all-purchasable-items"></a>
### 7. Inquiry All Purchasable Items { #inquiry-all-purchasable-items }

Retrieves all purchasable items.

**[Method]**
```java
public void queryItems(Activity activity, PurchaseListCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | Current activity of the application |
| PurchaseCallback | callback | Callback that returns the API request result |

**[Example Code]**

```java
InAppPurchases.InAppPurchase.queryItems(activity, new InAppPurchase.ItemListCallback() {
    @Override
    public void onCallback(JSONArray result, InAppPurchaseException exception) {
        if (exception != null) {
            // An error occurred, we need to handle the error
            return;
        }
        // Success! Include your code to handle the results here
    }
});
```

**[Response Example]**

```json
[
    {
        "itemSeq" : 1000208,
        "itemName" : "Test item 01",
        "marketItemId": "item01",
        "price": 1000,
        "currency": "KRW",
        "localizedPrice":"₩1,000"
    },
    {
        "itemSeq" : 1000209,
        "itemName" : "Test item 02",
        "marketItemId": "item02",
        "price": 7.99,
        "currency": "USD",
        "localizedPrice":"$7.99"
}]
```

<br/>

<a id="batch-process-of-unconsumed-payment"></a>
### 8. Batch Process of Unconsumed Payment { #batch-process-of-unconsumed-payment }

Batch reprocesses unprocessed payments (IAP server verification failures).

**[Method]**
```java
public void processesIncompletePurchases(Activity activity, IncompletePurchasesCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | Current activity of the application |
| IncompletePurchasesCallback | callback | Callback that returns the API request result |

**[Example Code]**

```java
InAppPurchases.InAppPurchase.processesIncompletePurchases(activity, new InAppPurchase.IncompletePurchasesCallback() {

    @Override
    public void onCallback(JSONObject result, InAppPurchaseException exception) {
           if (exception != null) {
              // An error occurred, we need to handle the error
              return;
           }
           // Success! Include your code to handle the results here }
});
```
**[Response Example]**

```json
{
    "successList": [
    	{
    		"paymentSeq" : "2014082510002163",
    		"purchaseToken" : "8nkx3SzHKlI74vmgQLzHExmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoB-AB",
    		"itemSeq" : 1000208,
    		"marketItemId"	: "item01",
    		"currency" : "KRW",
    		"price" : 1000.0
    	},
    	{
    		"paymentSeq" : "2014082510002164",
    		"purchaseToken" : "8nkx3SzATKlI74vmgQLzHExmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBaAC",
    		"itemSeq" : 1000209,
    	    "marketItemId"	: "item02",
    		"currency" : "KRW",
    		"price" : 1000.0
    	}
    ],
    "failList": [
    	{
    		"paymentSeq" : "2014082510002165",
    		"purchaseToken" : null,
    		"itemSeq" : 1000210,
    		"marketItemId"	: "item03",
    		"currency" : "KRW",
    		"price" : 1000.0
    	}
    ]
}
```

<br/>

<a id="payment-consume"></a>
### 9. Payment Consume { #payment-consume }
The user application server must notify the IAP server to consume the payment before issuing items.
Refer to the following for the API for payment consumption.

> [Note]  
> [Payment Consume API](/Mobile Service/IAP/en/api-guide/#payment-consume-api)

<a id="processing-error-after-calling-api"></a>

## Error Handling { #processing-error-after-calling-api }

<a id="public-class-inapppurchaseexception-extends-exception"></a>
### 1. InAppPurchaseException { #public-class-inapppurchaseexception-extends-exception }
Delivers error information for API calls.
If InAppPurchaseException is not `null`, the situation is treated as a failure.

|Method Name|Return type|Description|
|---|---|---|
|getErrorCode|Integer|Returns the error code.|
|getMessage|String|Returns detailed error information.|

> [Note]  
> [Error Code Details](/Mobile%20Service/IAP/en/error-code/)

**[Example Code]**  
```java
InAppPurchases.InAppPurchase.queryItems(activity, new InAppPurchase.ItemListCallback() {
    @Override
    public void onCallback(JSONArray result, InAppPurchaseException exception) {
        if (exception != null) {
            int errorCode = exception.getErrorCode();
              String errorMessage = exception.getMessage();
              // TODO : do something when error occurs.
              ....
            return;
        }
        // Success! Include your code to handle the results here
    }
});
```