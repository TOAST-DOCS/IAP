<!-- machine_translated: true -->

<a id="mobile-service-iap-android-sdk-guide"></a>

## Mobile Service > IAP > Android SDK 사용 가이드 { #mobile-service-iap-android-sdk-guide }

> [公告]<br>
> サブスクリプション決済をサポートする新しい IAP SDK が [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/) としてリリースされました。<br>
> 既存の IAP SDK では新機能の開発は行わない予定です。

<a id="development-environment"></a>

## 開発環境 { #development-environment }
* Android Studio IDE 2.3.3 以上
* Android SDK Version は **2.3.3 (API Level 10)** 以上

使用するオープンソース情報は次のとおりです。

|Name|Reference|Version|License|
|---|---|---|---|
|okhttp|http://square.github.io/okhttp/|1.5.4|Apache License 2.0|
|gson|https://code.google.com/p/google-gson/|2.2.4|Apache License 2.0|

<a id="using-in-android-studio-gradle"></a>

## Android Studio & Gradle 環境での使用 { #using-in-android-studio-gradle }

`NHN Cloud IAP SDK` は Gradle を基盤とした Android Studio IDE の開発環境を提供します。
jCenter Maven Repository からリモートでダウンロードできます。
以下のように、プロジェクトの build.gradle ファイルに repository と dependency の定義を追加します。

<a id="gradle-repository"></a>
### 1. Gradle Repository { #gradle-repository }

```
buildscript {
    repositories {
        jcenter()
    }
}
```

`NHN Cloud IAP SDK` で共通して使用される権限は次のとおりです。

|Permission|Description|
|---|---|
|android.permission.INTERNET|アプリケーションがネットワークソケットを開くことを許可します。|
|com.android.vending.BILLING|アプリケーションにアプリ内課金の権限を付与します。|

<br/>

<a id="adding-dependencies"></a>
### 2. 依存関係の追加 { #adding-dependencies }
<a id="adding-dependencies-google-play-store"></a>
#### Google Play Store
```
dependencies {
    implementation 'com.toast.iap:iap:1.5.0'
}
```
<a id="adding-dependencies-sdk-v17-api-v5---recommended"></a>
#### SDK v17 (API v5) - 推奨
```
dependencies {
    implementation 'com.toast.iap:iap-onestore:1.5.0'
}
```
追加される権限は次のとおりです。

|Permission|Description|
|---|---|
|android.permission.ACCESS_NETWORK_STATE|アプリケーションがネットワークに関する情報にアクセスできるようにします。|

<a id="adding-dependencies-sdk-v16-api-v4"></a>
#### SDK v16 (API v4)
```
dependencies {
    implementation 'com.toast.iap:iap-tstore:1.5.0'
}
```

<br/>

> [参考]  
> Release History   
> SDK のバージョン変更履歴はパッケージ内の RELEASE-NOTES.md を参照してください。

<a id="one-store-configuration-information"></a>

## One Store 設定情報 { #one-store-configuration-information }
2018年6月12日（火）より、旧バージョン SDK v16 (API v4) 以下が適用された新規アプリの登録ができなくなります。  
新規アプリを開発される場合は SDK v17 (API v5) をご使用ください。  

* [インアプリ SDK v15.xx.xx バージョン未満適用商品のサポート終了案内](https://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?page.no=1&orderValue=&orderType=&noticeId=31245&noticeNo=789&pageFlag=List&searchValue=)  
* [旧バージョン IAP SDK 適用新規アプリ登録不可案内](https://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?page.no=1&orderValue=&orderType=&noticeId=31224&noticeNo=788&pageFlag=List&searchValue=)  

<a id="sdk-v17-api-v5"></a>
### 1. SDK v17 (API v5) { #sdk-v17-api-v5 }
<a id="sdk-v17-api-v5-promoting-one-store-update-and-installation"></a>
#### One Store のアップデートおよびインストールの誘導
SDK のエラーコード `INAPP_ONESTORE_NEED_UPDATE(201)` が発生した場合、以下のコードでインストールを誘導できます。
```java
Intent intent = new Intent("android.intent.action.VIEW");
intent.setData(Uri.parse("http://m.onestore.co.kr/mobilepoc/etc/downloadGuide.omp"));
startActivity(intent);
```

<a id="sdk-v17-api-v5-requesting-one-store-login"></a>
#### One Store へのログインリクエスト
`NHN Cloud IAP SDK` では内部的にログイン状態を確認するため、別途ログイン処理を行う必要はありません。
使用中にログインされていない場合、One Store ログインポップアップ（はい/いいえ）が表示されます。
ログインポップアップで `はい` を選択すると One Store ログイン画面に遷移し、`いいえ` を選択すると `INAPP_ONESTORE_NEED_LOGIN(202)` エラーが発生します。

>[参考]  
>[One Store へのログインリクエスト](https://dev.onestore.co.kr/devpoc/reference/view/IAP_v17_05_implementation#HC6D0C2A4D1A0C5B4B85CADF8C778C694CCADD558AE30-getLoginIntent2829)

<a id="sdk-v17-api-v5-using-popup-payment-screen"></a>
#### ポップアップ決済画面用の使用
ポップアップ形式の決済画面を使用する場合は、`AndroidMenifest.xml` に以下の設定を追加してください。
```xml
<application>
    <meta-data 
        android:name="iap:view_option" 
        android:value="popup | full" />
</application>
```
> [参考]   
> [OneStore - インアプリ決済適用のための事前準備 > 7. Android Manifest ファイル設定](https://dev.onestore.co.kr/devpoc/reference/view/IAP_v17_04_preparation#HAndroidManifestD30CC77CC124C815) 

<a id="sdk-v16-api-v4"></a>
### 2. SDK v16 (API v4) { #sdk-v16-api-v4 }
決済テストの場合は、以下の設定を `AndroidMenifest.xml` に追加してください。  
```
<application>
    <meta-data 
        android:name="iap:plugin_mode" 
        android:value="development" />
</application>
```

<a id="implementing-sample-application"></a>

## サンプルアプリケーションの提供 { #implementing-sample-application }

IAP Android SDK では、Google Play Store および One Store 向けのサンプルアプリケーションを提供しています。
サンプルアプリケーションを使用して、IAP Android SDK が提供する機能を簡単にテストできます。

> [参考]  
> テスト前の注意事項   
> 決済テストの前に [コンソール使用ガイド](/Mobile Service/IAP/ja/console-guide/) を熟読のうえ、コンソール環境の構成を先に進めてください。

<a id="import-project"></a>
### 1. Import Project { #import-project }

配布された SDK パッケージ内の `/sample` ディレクトリを Android Studio で `Import Project` します。

<a id="setting-market-information-to-androidmanifestxml"></a>
### 2. AndroidManifest.xml 情報設定 { #setting-market-information-to-androidmanifestxml }

IAP Web Console に登録した `Store APP ID` をサンプルアプリケーションの applicationId と同じ値に設定します。
```
android {
    defaultConfig {
        applicationId "your app id"
    }
}
```

> [参考]  
> applicationId   
> 必ず実際のストア（Google Play Store、One Store）の情報と一致させる必要があります。


<a id="android-reference"></a>

## API Reference { #android-reference }

<a id="activating-log-information"></a>

### 1. ログ情報の有効化 { #activating-log-information }

デバッグ用のログ情報の出力を有効化します。

**[Method]**
```java
public void setDebugMode(boolean isDebuggable);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Boolean | isDebuggable | デバッグログの出力有無 |

**[Example Code]**  

```java
InAppPurchases.InAppPurchase.setDebugMode(true);
```

<br/>

<a id="store-market-settings"></a>

### 2. ストア（マーケット）設定 { #store-market-settings }

SDK の初期化時に使用するストア（マーケット）を設定します。

**[ストア別マーケット ID]**

|MarketId|Store|
|---|---|
|GG|Google Play Store|
|TS|One Store SDK V16 (API V4) - 旧 TStore|
|ONESTORE|One Store SDK V17 (API V5)|

**[Method]**

```java
public boolean registerMarketId(String marketId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| String | marketId | マーケット ID |

**[Example Code]**  

`AndroidMenifest.xml` ファイルで設定する場合：
```xml
<meta-data 
    android:name="com.toast.iap.config.market" 
    android:value="GG" />
```
`Java` コードで設定する場合：
```java
InAppPurchases.InAppPurchase.registerMarketId(marketId); // marketId : String value
```

<br/>

<a id="registering-app-id"></a>

### 3. App ID 登録 { #registering-app-id }

IAP Android SDK を使用するためのサービス ID です。
App ID は `NHN Cloud Console > Mobile Service > IAP` で確認できます。

**[Method]**

```java
public boolean registerAppId(long appId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Long | appId | NHN Cloud コンソールの IAP Service で発行された App ID |

**[Example Code]**  

`AndroidMenifest.xml` ファイルで設定する場合：
```xml
<meta-data 
    android:name="com.toast.iap.config.appId" 
    android:value="1234567" />
```
`Java` コードで設定する場合：
```java
InAppPurchases.InAppPurchase.registerAppId(1234567);// appId : long integer
```
<br/>

<a id="registering-user-identifier"></a>

### 4. ユーザー登録 { #registering-user-identifier }

認証が完了したユーザー ID を登録します。
開発会社で定義したユーザー識別キーであり、アイテムが付与される対象です。

**[Method]**

```java
public boolean registerUserId(String userId);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| String | userId | ユーザー ID 識別子 |

**[Example Code]**  

```java
InAppPurchases.InAppPurchase.registerUserId(userId); // userId : String value
```

<br/>

<a id="request-payment"></a>

### 5. 決済リクエスト { #request-payment }

クライアントからアイテムの購入をリクエストします。
決済リクエストに対するレスポンスは PurchaseCallback を通じて受け取ります。
決済が正常に完了したら、結果値をサーバーに送信して [9. 決済消費](/Mobile%20Service/IAP/ja/android-sdk-guide/#9) を行う必要があります。

> [参考]  
> アプリ内課金は決済リクエストと決済消費の 2 段階で進行します。  
> [IAP 決済フロー](/Mobile%20Service/IAP/ja/Overview/#iap)  

**[Method]**
```java
public void requestPurchase(Activity activity, long itemId, PurchaseCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | アプリケーションの現在のアクティビティ |
| Long | itemId | Web Console で発行されたアイテム ID |
| PurchaseCallback | callback | API リクエスト結果を伝えるコールバック |

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

### 6. 未消費決済履歴照会 { #inquiry-unconsumed-user-payment-history }

ユーザーの消費（Consume）されていない決済履歴を照会します。

**[Method]**
```java
public void queryPurchases(Activity activity, PurchaseListCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | アプリケーションの現在のアクティビティ |
| PurchaseCallback | callback | API リクエスト結果を伝えるコールバック |

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

### 7. 購入可能アイテム一覧照会 { #inquiry-all-purchasable-items }

購入可能なすべてのアイテム一覧を照会します。

**[Method]**
```java
public void queryItems(Activity activity, PurchaseListCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | アプリケーションの現在のアクティビティ |
| PurchaseCallback | callback | API リクエスト結果を伝えるコールバック |

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

### 8. 未処理決済件の一括再処理 { #batch-process-of-unconsumed-payment }

未処理の決済件（IAP サーバー検証失敗）に対して一括で再処理を行います。

**[Method]**
```java
public void processesIncompletePurchases(Activity activity, IncompletePurchasesCallback callback);
```

**[Parameter]**

|Type|Name|Description|
|---|---|---|
| Activity | activty | アプリケーションの現在のアクティビティ |
| IncompletePurchasesCallback | callback | API リクエスト結果を伝えるコールバック |

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

### 9. 決済消費 { #payment-consume }

ユーザーアプリケーションサーバーは、アイテムを付与する前に IAP サーバーへ決済を消費することを通知する必要があります。
決済消費用の API については以下を参照してください。

> [参考]  
> [Payment Consume API](/Mobile Service/IAP/ja/api-guide/#payment-consume-api)

<a id="processing-error-after-calling-api"></a>

## エラー処理 { #processing-error-after-calling-api }

<a id="public-class-inapppurchaseexception-extends-exception"></a>

### 1. InAppPurchaseException { #public-class-inapppurchaseexception-extends-exception }

API 呼び出しに対するエラー情報を伝えます。
InAppPurchaseException が `null` でない場合は失敗として処理します。

|Method Name|Return type|Description|
|---|---|---|
|getErrorCode|Integer|エラーコードを返します。|
|getMessage|String|エラーの詳細情報を返します。|

> [参考]  
> [エラーコード詳細](/Mobile%20Service/IAP/ja/error-code/)

**[Example Code]**  
```java
InAppPurchases.InAppPurchase.queryItems(activity, new InAppPurchase.ItemListCallback() {
    @Override
    public void onCallback(JSONArray result, InAppPurchaseException exception) {
        if (exception != null) {
            int errorCode = exception.getErrorCode();
              String errorMessage = exception.getMessage();
              // TODO : エラー発生時の処理を定義します。
              ....
            return;
        }
        // Success! Include your code to handle the results here
    }
});
```