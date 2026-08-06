<!-- machine_translated: true -->

<a id="mobile-service-iap-galaxy-store-console-guide"></a>
## Mobile Service > IAP > Galaxy Store Console Guide { #mobile-service-iap-galaxy-store-console-guide }

IAPでGalaxy Storeを連携するには、アプリ登録時にPackageName と IAP Public Key を入力する必要があります。

<a id="check-package-name"></a>
## Pakcage Name 確認する { #check-package-name }
* [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as) でバイナリファイルを登録後、パッケージ名を確認します。
* Galaxy Store Seller Portal > アプリ > アプリを選択 > バイナリ
 ![[]](http://static.toastoven.net/prod_iap/2020/galaxy_app_kr.png)

<a id="generate-iap-public-key"></a>
## IAP Public Keyを生成する { #generate-iap-public-key }
> **注記**
> [https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal](https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal)

* [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as) > セラーサポート > IAP サービス > IAP Key > IAP Key を作成

<a id="enter-information-in-the-iap-console"></a>
## IAPコンソールで情報を入力する { #enter-information-in-the-iap-console }
[NHN Cloud コンソール](https://console.nhncloud.com)で組織とプロジェクトを選択し、**Mobile Service** > **IAP** > **App** > **追加**、またはAppを選択して**編集**をクリックします。
* **Store APP ID**: Galaxy StoreアプリのPackage Nameを入力します。
* **IAP Public Key**: IAP Keyで生成したPublic Keyを入力します。
![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_iap_console_app.png)

<a id="register-real-time-server-notifications-isn"></a>
## リアルタイムサーバー通知（ISN）の登録 { #register-real-time-server-notifications-isn }
* アプリ > アプリを選択 > **In App Purchase** > 詳細 > **リアルタイムサーバー通知 (ISN)**

![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_isn.png)

- ISN url: `https://api-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive`
    - Gamebase サンドボックスを使用している場合、ISN url は `https://sandbox-api-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive` を入力します。