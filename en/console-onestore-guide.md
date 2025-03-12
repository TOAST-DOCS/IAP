## Mobile Service > IAP > ONE Store Console Guide

Create your license key and OAuth credentials in the one-store to register for the IAP app information.

### Create One-Store Key
```
Apps > select App> In-App > Managed Product > Managed In-App API
```

![In-App API 관리](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_01.png)

![NHN Cloud IAP 앱 설정](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_iap_console_01.png)

| Key                     | Description                       |
|-------------------------|-----------------------------------|
| **Store ID**              | **ONESTORE**                      |
| **App Name**                | App Name                          |
| **ONE Store API Version**     | **OneStore API V7**             |
| **ONE Store Client ID**     | ONE Store Oauth **Client ID**           |
| **ONE Store Client Secret** | ONE Store Oauth **Client Secret** |
| **ONE Store License Key**   | **License Key**   |



### Set up ONE store Notifications for Real-Time Subscription Status

```
Apps > Select App > In-App Information > Subscriptions > PNS Management > Subscription Status Notifications
```

![PNS Management](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_02.png)

- Server URL: `https://gw-iap.nhncloudservice.com/market-notifications/ONESTORE/{ONE Store Client ID}/receive`
    - If using Gamebase Sandbox, enter `https://sandbox-gw-iap.nhncloudservice.com/market-notifications/ONESTORE/{ONE Store Client ID}/receive` for the server URL
- The policy for sending subscription status notifications can be found in the [ONE store In-App SDK Guide](https://onestore-dev.gitbook.io/dev/tools/tools/v21/07.-pns-push-notification-service).

> The subscription feature is supported starting with version V21 of the ONE Store In-App Payment SDK.