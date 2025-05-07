## Mobile Service > IAP > ONE Store 콘솔 가이드

원스토어에서 라이선스 키 및 OAuth 인증 정보를 생성하여 IAP 앱 정보에 등록합니다.

### 원스토어 키 생성
```
Apps > 앱 선택 > In-App정보 > 관리상품 > In-App API 관리
```

![In-App API 관리](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_01.png)

![NHN Cloud IAP 앱 설정](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_iap_console_02.png)

[표] 원스토어 V7(V21) 연동을 위한 앱 등록 필드

| 필드                          | 설명                                  |
|-----------------------------|-------------------------------------|
| **Store ID**                | 스토어 리스트에서 **ONESTORE** 선택           |
| **App Name**                | IAP Console에서 사용할 이름                |
| **ONE Store API Version**   | 리스트에서 **OneStore API V7** 선택        |
| **ONE Store Package Name**  | 스토어에 등록한 어플리케이션의 **패키지명**           |
| **ONE Store Client ID**     | 스토어 Oauth 인증 정보 중 **Client ID**     |
| **ONE Store Client Secret** | 스토어 Oauth 인증 정보 중 **Client Secret** |
| **ONE Store License Key**   | **License Key**                     |


### 실시간 구독 상태 수신을 위한 원스토어 알림 설정

```
Apps > 앱 선택 > In-App정보 > 구독상품 > PNS 관리 > 구독 상태 알림
```

![PNS 관리](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_onestore/onestore_console_02.png)

- 서버 URL: `https://gw-iap.nhncloudservice.com/market-notifications/ONESTORE/{ONE Store Package Name}/receive`
    - Gamebase 샌드박스를 사용할 경우 서버 URL은 `https://sandbox-gw-iap.nhncloudservice.com/market-notifications/ONESTORE/{ONE Store Package Name}/receive` 입력
- 구독 상태 알림 전송 정책은 [원스토어 In-App SDK 가이드](https://onestore-dev.gitbook.io/dev/tools/tools/v21/07.-pns-push-notification-service)에서 확인할 수 있습니다.
   
> 구독 기능은 원스토어 인앱결제 SDK V21 버전부터 지원합니다. 
