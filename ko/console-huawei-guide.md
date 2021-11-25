## Mobile Service > IAP > Huawei AppGallery 콘솔 가이드

> [공지]
> 구독 결제를 지원하는 신규 IAP SDK가 [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)로 출시됐습니다.
> 기존 IAP SDK는 더 이상 신규 기능을 개발하지 않을 예정입니다.
> 본 문서는 [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/) 가이드입니다.

## Huawei Developer Console
1. [화웨이 개발자 콘솔](https://developer.huawei.com/consumer/en/console) 상에 계정을 등록 후 <br/>
에코시스템 서비스 / 앱 서비스 -> [AppGallery Connect 콘솔](https://developer.huawei.com/consumer/en/service/josp/agc/index.html#/) 로 진입합니다.
   ![[]](http://static.toastoven.net/prod_iap/huawei_console_kor.png)
2. [AppGallery Connect 콘솔](https://developer.huawei.com/consumer/en/service/josp/agc/index.html#/) 에서 My Apps 메뉴로 진입하면 신규 앱 등록 / 기존 앱 관리를 할 수 있습니다.
   ![[]](http://static.toastoven.net/prod_iap/huawei_console_app_main_eng.png)
   ![[]](http://static.toastoven.net/prod_iap/huawei_console_app_01_eng.png)
3. NHN Cloud IAP 는 화웨이 스토어 연동은 안드로이드 APK 패키지 타입과 모바일 디바이스 만을 지원합니다.<br/>
또한, 앱은 최종적으로 프로젝트에 연동되어 있어야 하므로, 미리 첫 생성할 때부터 프로젝트를 함께 생성하던지, 기존에 생성되어 있는 프로젝트를 선택하여 연동시켜 놓으셔야 합니다.
   ![[]](http://static.toastoven.net/prod_iap/huawei_console_app_02_eng.png)
5. 앱 생성 후 추가적인 정보를 입력하고, 화웨이 개발자 센터에서 확인할 수 있는 정보 값을 NHN Cloud IAP 콘솔의 앱 설정에 입력해 줘야 합니다.
6. 본 가이드의 내용은 아마존 앱스토어에 등록된 앱의 정보와 NHN Cloud IAP 간의 앱 정보를 연결하기 위한 정보만을 다루고 있으며, <br/> 보다 자세한 화웨이 앱갤러리의 앱 등록 절차에 대해서는 [아마존의 가이드 문서](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/introduction-0000001050033062) 를 참조하시기 바랍니다.

## 연결을 위해 필요한 설정 값들
![[]](http://static.toastoven.net/prod_iap/huawei_iap_console_kor.png)
### Store App ID
- AppGallery Connect > MyProject > Project Settings 화면에서 앱과 연결된 프로젝트 관련 정보들을 확인할 수 있습니다.
- 이 화면의 `App Information - Package Name` 값을 NHN Cloud IAP 콘솔 앱 설정의 `Store App ID` 에 입력해야 합니다.
  - 이 값은 AppGallery Connect > MyApp > App 화면에서도 확인할 수 있습니다. 

![[]](http://static.toastoven.net/prod_iap/huawei_console_app_06_eng.png)

### Huawei App ID & App Secret
- AppGallery Connect > MyProject > Project Settings 화면에서 앱과 연결된 프로젝트 관련 정보들을 확인할 수 있습니다.
- 이 화면의 `App Information - OAuth 2.0 Client ID` 값을 NHN Cloud IAP 콘솔 앱 설정의 `Huawei App ID` 값으로 입력해야 합니다.
- 이 화면의 `App Information - OAuth 2.0 Client Secret` 값을 NHN Cloud IAP 콘솔 앱 설정의 `Huawei App Secret` 값으로 입력해야 합니다. 

![[]](http://static.toastoven.net/prod_iap/huawei_console_app_06_eng.png)

### Huawei Developer Public Key
- AppGallery Connect > MyProject > Earn > In-App Purchases 화면에서 IAP 관련 정보를 확인할 수 있습니다.
- 처음 이 화면에 진입하면 IAP 를 활성화시키는 버튼을 눌러 IAP 를 활성해주면, 생성된 `Public Key` 값을 확인할 수 있으며,<br/>
이 값을 NHN Cloud IAP 콘솔 앱 설정의 `Huawei Developer Public Key` 값으로 입력해야 합니다. 

![[]](http://static.toastoven.net/prod_iap/huawei_console_app_05_eng.png)