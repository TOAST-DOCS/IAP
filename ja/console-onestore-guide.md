<!-- pre-align:aligned sig=42ad6ead3e45 -->

<a id="mobile-service-iap-one-store-console-guide"></a>
## Mobile Service > IAP > ONE Store Console Guide { #mobile-service-iap-one-store-console-guide }

Create your license key and OAuth credentials in the one-store to register for the IAP app information.

<a id="create-one-store-key"></a>
### Create One-Store Key { #create-one-store-key }
```
Apps > select App> In-App > Managed Product > Managed In-App API
```

![In-App API管理](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_01.png)

![NHN Cloud IAPアプリ設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_iap_console_02.png)

| Key                     | Description                       |
|-------------------------|-----------------------------------|
| **Store ID**                | ストアリストから**ONESTORE**選択           |
| **App Name**                | IAPコンソールで使用する名前                    |
| **ONE Store API Version**   | リストから**OneStore API V7**選択        |
| **ONE Store Package Name**  | ストアに登録したアプリケーションの**パッケージ名**           |
| **ONE Store Client ID**     | ストアOauth認証情報のうち**Client ID**     |
| **ONE Store Client Secret** | ONE Store Oauth **Client Secret** |
| **ONE Store License Key**   | **License Key**                     |


<a id="set-up-one-store-notifications-for-real-time-subscription-status"></a>
### リアルタイム購読状態を受信するためのONEstore通知設定 { #set-up-one-store-notifications-for-real-time-subscription-status }

```
Apps > アプリ選択 > In-App情報 > 購読商品 > PNS管理 > 購読状態通知
```

![PNS管理](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_03.png)

- サーバーURL: `https://api-iap.nhncloudservice.com/markets/ONESTORE/notification/{ONE Store Package Name}/receive`
    - Gamebaseサンドボックスを使用する場合、サーバーURLは`https://sandbox-api-iap.nhncloudservice.com/markets/ONESTORE/notification/{ONE Store Package Name}/receive`入力
- 購読状態通知送信ポリシーは[ONEstore In-App SDKガイド](https://onestore-dev.gitbook.io/dev/eng/tools/tools/v21/pns)で確認できます。

> 購読機能はONEstoreアプリ内決済SDK V21バージョンからサポートします。
