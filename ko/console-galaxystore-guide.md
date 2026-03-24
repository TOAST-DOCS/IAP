## Mobile Service > IAP > Galaxy Store 콘솔 가이드

IAP 에서 Galaxy Store 연동을 하려면 앱 등록 시, PackageName과 IAP Public Key를 입력해야 합니다.

## Package Name 확인하기
* [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as) 에서 바이너리 파일 등록 후, 패키지명을 확인합니다.
* Galaxy Store Seller Portal > 앱 > 앱 선택 > 바이너리
 ![[]](http://static.toastoven.net/prod_iap/2020/galaxy_app_kr.png)

## IAP Public Key 생성하기
> **참고**
> [https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal](https://developer.samsung.com/iap/isn/requirements.html#Create-an-IAP-key-in-Seller-Portal)

* [Galaxy Store Seller Portal](https://seller.samsungapps.com/main/sellerMain.as) > 셀러지원 > IAP 서비스 > IAP Key > IAP Key 만들기

## IAP 콘솔에서 정보 입력하기
* [콘솔](https://console.nhncloud.com)에서 조직 및 프로젝트를 선택하고 **Mobile Service** > **IAP** > **App** > **추가** 또는 App을 선택하고 **편집**을 클릭
* Store APP ID: Galaxy Store 앱 Package Name 입력
* IAP Public Key: IAP Key에서 생성한 Public Key 입력
![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_iap_console_app.png)

## 실시간 서버 알림 (ISN) 등록
```
앱 > 앱 선택 > In App Purchase > 더보기 > 실시간 서버 알림 (ISN)
```

![[]](https://static.toastoven.net/prod_iap/console_galaxy/galaxy_isn.png)

- ISN url: `https://gw-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive`
    - Gamebase 샌드박스를 사용하고 있다면 ISN url은 `https://sandbox-gw-iap.nhncloudservice.com/markets/GALAXY/notification/{Galaxy Store Package Name}/receive` 입력
