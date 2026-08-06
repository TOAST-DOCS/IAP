<!-- machine_translated: true -->

<a id="mobile-service-iap-galaxy-store-console-guide"></a>
## Mobile Service > IAP > Galaxy Store Console Guide { #mobile-service-iap-galaxy-store-console-guide }

To use Galaxy Store in IAP, you must enter the PackageName and IAP Public Key when registering an app.

<a id="check-package-name"></a>
## Check Package Name { #check-package-name }
* After registering the binary file in [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as), check the package name.
* Galaxy Store Seller Portal > App > Select App > Binary
 ![[]](http://static.toastoven.net/prod_iap/2020/galaxy_app_kr.png)

<a id="generate-iap-public-key"></a>
## Generate IAP Public Key { #generate-iap-public-key }
> **Note**
> [https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal](https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal)

* [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as) > Seller Support > IAP Service > IAP Key > Create IAP Key

<a id="enter-information-in-the-iap-console"></a>
## Enter Information in the IAP Console { #enter-information-in-the-iap-console }
In the [NHN Cloud console](https://console.nhncloud.com), select the organization and project, and go to **Mobile Service** > **IAP** > **App** > **Add**, or select an app and click **Edit**.
* **Store APP ID**: Enter the Galaxy Store app Package Name
* **IAP Public Key**: Enter the Public Key generated from IAP Key
![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_iap_console_app.png)

<a id="register-real-time-server-notifications-isn"></a>
## Register Real-time Server Notifications (ISN) { #register-real-time-server-notifications-isn }
* App > Select App > **In App Purchase** > More > **Real-time Server Notifications (ISN)**

![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_isn.png)

- ISN url: `https://api-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive`
    - If you're using the Gamebase sandbox, enter the ISN url as `https://sandbox-api-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive`