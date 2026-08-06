<!-- pre-align:aligned sig=e8dca5bc8151 -->

<a id="mobile-service-iap-ios-sdk-guide"></a>
## Mobile Service > IAP > iOS SDK Guide { #mobile-service-iap-ios-sdk-guide }

> [Notice]
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).
> No new features will be developed for the existing IAP SDK.


<a id="development-environment"></a>
## Development Environment { #development-environment }

* OSX is required
* Xcode 6.0.1 and higher
* IAP SDK Support for iOS 6.x and higher

Add below framework to application to use IAP SDK. 

| Name                 | Description                                             |
| ------------------ | ---------------------------------------------- |
| StoreKit.framework | Framework for in-app purchase sync in App Store          |
| libsqlite3.tbd     | TOAST Cloud IAP SDK uses sqlite for managing local data |
| coreTelephony.framework   | This is for acquiring user’s country information. |

> [Reference]  
> Suppose you have completed registering application/ item to iTunes Connect in order to test in-app purchase.    
> [iTunes Connect](http://itunesconnect.apple.com)

<a id="iap-console"></a>
## IAP Console { #iap-console }

<a id="1-store-registration---getting-app-id"></a>
### 1\. Store Registration - Getting APP ID { #1-store-registration---getting-app-id }

```
1. select [App] tab >  click [Add] button  
2. select AS(Apple Store) in [Store ID]  
    - Market APP ID : Apple App Store Bundle Id
3. check [APP ID].
```

![[Figure 1 Getting APP ID]](http://static.toastoven.net/prod_iap/iap_n_32.png)
<center>[Figure 1 Getting APP ID]</center>

<a id="2-item-registration"></a>
### 2\. Item Registration { #2-item-registration }

```
1. select [Item] tab > click [Add] button  
2. select AS(Apple Store) in [Store ID]  
3. register item  
    - Item Name : item name 
    - Store Item ID : item Product ID registered in iTunes Connect
4. check [ITEM]
```

<a id="setting-xcode-project"></a>
## Setting Xcode Project { #setting-xcode-project }


| Directory Name    | Description                        |
| -------- | ------------------------- |
| /docs    | IAP iOS SDK API Reference |
| /lib     | Framework                 |
| /samples | Sample Application        |
<center>[Table. 1 iOS SDK Directory]</center>

<a id="1-add-iap-sdk-and-framework"></a>
### 1\. Add IAP SDK and framework { #1-add-iap-sdk-and-framework }

```
1. [Xcode] > [Project] > [Targets – Build Phases]  
2. Add the following frameworks to [Link Binary With Libraries]  
    - libsqlite3.tbd
    - TIAPurchase.framework
    - StoreKit.framework  
    - CoreTelephony.framework
```

![[Figure 2 Add library for IAP]](http://static.toastoven.net/prod_iap/iap_51.png)
<center>[Figure 2 Add library for IAP]</center>

<a id="2-setting-plist"></a>
### 2\. Setting plist { #2-setting-plist }

```
Create string value with TOAST_IAP_APP_ID key to [plist] and enter app ID.  
Once completed, .plist will be in the following format.
```

![[Figure 3 Set App ID to plist]](http://static.toastoven.net/prod_iap/iap_19.jpg)
<center>[Figure 3 Set App ID to plist ]</center>

> [Reference - Setting iOS9 ATS]  
> Apply ATS (App Transport Security) setting from iOS9 SDK
> When building in system beyond XCode7, you need to set exceptions for certain IAP domains as below.   
> [Apple Document](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/)

```xml
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSExceptionDomains</key>
        <dict>
            <key>api-iap.cloud.toast.com</key>
            <dict>
                <key>NSIncludesSubdomains</key>
                <true/>
                <key>NSExceptionAllowsInsecureHTTPLoads</key>
                <true/>
                <key>NSExceptionRequiresForwardSecrecy</key>
                <false/>
            </dict>
        </dict>

    </dict>
```

<a id="api-reference"></a>
## API Reference { #api-reference }

<a id="1-import-header-file"></a>
### 1\. Import Header File { #1-import-header-file }

If you are ready to use SDK in application, add header file to IAP SDK as below.

``` objc
#import "TIAPurchase.h"
```

<a id="2-enable-log"></a>
### 2\. Enable Log { #2-enable-log }

Activate log information exposure for debugging. 

[Example Code]

``` objc
[TIAPurchase setDebugMode:YES];
```

<a id="3-register-user"></a>
### 3\. Register User { #3-register-user }

Register user identifier value after user verification in application

[Example Code]

``` objc
NSError *purchaseError = nil;
BOOL result = {TIAPurchase registerUserId:@"user001" error:&purchaseError};
If (!result) {
    // An error occurred, we need to handle the error.
    NSLog(@"errorInfo = %@", purchaseError);
}
// register user id successfully.
```

<a id="4-request-payment"></a>
### 4\. Request Payment { #4-request-payment }

Send in-app purchase request. Once payment is successfully done, payment details will be sent via completionHandler.

[Example Code]

```objc
[TIAPurchase startPurchaseWithViewController:self itemId:1000004 completionHandler:^(id result, NSError *error) {

  if (error)
  {
      // An error occurred, we need to handle the error
      NSLog(@"purchase error, %@ %d", [error domain], [error code]);
      return;
  }
  else
  {
      /**
       Success! Include your code to handle the results here

       JSON data to 'NSDicionary', This is nil if there was an error.
       [keys]
       - paymentSeq : generated payment id
       - itemSeq : item id
       - purchaseToken : represent to token for consume by
server.
       - currency : represent to item currency
       - price : represent to item price.
       */

      NSDictionary *purchaseResult = result;
      NSLog(@"purchase success, purchase = %@", purchaseResult);
  }

}];
```

<a id="5-inquiry-unconsumed-payment"></a>
### 5\. Inquiry unconsumed payment { #5-inquiry-unconsumed-payment }

Inquire unconsumed payment history. 

[Example Code]

```objc
[TIAPurchase purchasesWithCompletionHandler:^(id result, NSError *error) {
    if (error)
    {
        // An error occurred, we need to handle the error
        NSLog(@"purchasesWithCompletionHandler occured error, %@ %d", [error domain], [error code]);
        return;
    }

    /**
     Success! Include your code to handle the results here

     JSON data to 'NSArray', This is nil if there was an error.
     [keys]
     - paymentSeq : generated payment id
     - itemSeq : item id
     - purchaseToken : represent to token for consume by server.
     - currency : represent to item currency.
     - price : represent to item price.
     */

    NSArray *purchases = result;
    NSLog(@"purchasesWithCompletionHandler, size:%d npurchases:%@", [purchases count], purchases);

}];
```

<a id="6-inquiry-all-purchasable-items"></a>
### 6\. Inquiry all purchasable items { #6-inquiry-all-purchasable-items }

Inquire all purchasable items

[Example Code]
```objc
[TIAPurchase itemListWithCompletionHandler:^(id result, NSError *error) {
    if (error)
    {
        // An error occurred, we need to handle the error
	NSLog(@"itemListWithCompletionHandler occured error, %@ %d", [error domain], [error code]);
        return;
    }

    /**
    Success! Include your code to handle the results here

    JSON data to 'NSArray', This is nil if there was an error.
    [keys]
    - itemSeq : item id
    - itemName : item name
    - usingStatus : item status on IAP server
    - regYmdt : item registration date on IAP server
    - appName : app name
    - marketId : market id (AS : APPLE STORE)
    - marketItemId : market item id (product id)
    - currency : represent to item currency
    - price : represent to item price
    - localizedPrice - represent to localized item price
    */

    NSArray *itemList = result;
    NSLog(@"itemListWithCompletionHandler, size:%lu \nitemList:%@", [itemList count], itemList);
}];
```

<a id="7-batch-process-of-unconsumed-payment"></a>
### 7\. Batch process of unconsumed payment { #7-batch-process-of-unconsumed-payment }

processes whole of unconsumed(cause of verification failure or network loss) payments.

[Example Code]
```objc
[TIAPurchase processesIncompletePurchasesWithCompletionHandler:^(id result, NSError *error) {
        if (error)
        {
            // An error occurred, we need to handle the error
           NSLog(@"processesIncompletePurchasesWithCompletionHandler occured error, %@ %d", [error domain], [error code]);
            return;
        }

        /**
         Include your code to handle the results here
         
         JSON data to 'NSDictionany'.
         [keys]
         - successList : success data list (NSArray)
                 [keys]
                 - paymentSeq : generated payment id
                 - itemSeq : represent item id
                 - purchaseToken : represent token for validation
                 - marketItemId : market item id (product id)
                 - currency : represent to item currency
                 - price : represent to item price

         - failList : fail data list (NSArray)
                 [keys]
                 - paymentSeq : generated payment id
                 - itemSeq : represent item id
                 - purchaseToken : represent token for validation
                 - marketItemId : market item id (product id)
                 - currency : represent to item currency
                 - price : represent to item price
         */
        NSDictionary *data = result;
        NSLog(@"processesIncompletePurchasesWithCompletionHandler data:%@", data);
}];
```

<a id="8-payment-consume"></a>
### 8\. Payment Consume { #8-payment-consume }
User application server should notify IAP server for payment consume before issuing item. Use Payment Purchase Token to check validity of the payment between user server and IAP server.

> [Reference]  
> [Payment Consume API](/Mobile Service/IAP/en/api-guide/#payment-consume-api)  


<a id="9-app-store-promoting-in-app-purchase"></a>
### 9\. App Store Promoting In-App Purchase { #9-app-store-promoting-in-app-purchase }
If you use App Store promoting in-app purchase, register your delegate and use payment details.<br>
`You must register delegate before initialize to receive payment history.`

[Example Code]
##### TIAPurchaseDelegate
```objc
@interface ViewController () <TIAPurchaseDelegate>
...
@end

// Delegate registration
[TIAPurchase setDelegate:self];

// Delegate implementation
- (void)didFinishPurchasingItemFromStore:(TIAPItem *)item
                              paymentSeq:(NSString *)paymentSeq
                           purchaseToken:(NSString *)purchaseToken
                               withError:(NSError *)error {
    
    if (error == nil) {
        NSLog(@"App Store promoting in-app purchase successful");
        
    } else {
        NSLog(@"App Store promoting in-app purchase failed");
    }
}
```
##### TIAPItem

```objc
@interface TIAPItem : NSObject

@property (nonatomic, copy, readonly) NSString *itemSeq;
@property (nonatomic, copy, readonly) NSString *storeId;
@property (nonatomic, copy, readonly) NSString *marketItemId;
@property (nonatomic, copy, readonly) NSString *currency;
@property (nonatomic, copy, readonly) NSDecimalNumber *price;
@property (nonatomic, copy, readonly) NSString *localizedPrice;

@end
```