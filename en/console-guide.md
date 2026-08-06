<!-- pre-align:aligned sig=0b5f52f37dd1 -->

<a id="mobile-service-iap-console-common-guide"></a>
## Mobile Service > IAP > Console Common Guide { #mobile-service-iap-console-common-guide }

To use IAP SDK, you first need to register app and item at web console after store registration.



<br>


<a id="project-creation"></a>
## Project Creation { #project-creation }
```
At NHN Cloud Console (https://console.toast.com), click [+ Create New Project]
```
![[]](http://static.toastoven.net/prod_iap/iap-console-new-project.png)


<a id="activating-iap"></a>
## Activating IAP { #activating-iap }
```
At NHN Cloud Console (https://console.toast.com), click [Mobile Service] > [IAP] 
```
![[]](http://static.toastoven.net/prod_iap/iap-console-iap-on.png)


<a id="check-appkey"></a>
## Check AppKey { #check-appkey }
```
Click [URL & Appkey] and check AppKey  or copy the key to clipboard.
```
![[]](http://static.toastoven.net/prod_iap/iap-console-appkey.png)


<a id="app-registration"></a>
## App Registration { #app-registration }
See Store console guide if you want store specific setting.
```
1. Select [App] Tab and Click [Add]
2. Select [Store ID] 
3. Common Information
   - Store ID : Google, Apple, ONE Store
   - App Name : Your App Name
   - Store APP ID : Store package name or bundle id
4. Click [Add] button. 
```
![[]](http://static.toastoven.net/prod_iap/iap_reg_app_en.png)

<a id="item-registration"></a>
## Item Registration { #item-registration }
```
1. Click [Item] Tab.  
2. Select [Store ID] and Click [+ Add]   
3. Register item name in [Item Name]  
4. Register store item id in [Store Item ID]
5. Select [Product Type] : CONSUMABLE , AUTO_RENEWABLE
6. Select [Status]  
7. Click [Add] and check [ITEM ID].  
```

![[]](http://static.toastoven.net/prod_iap/iap-console-new-item.png)

<a id="product-type"></a>
## Product Type { #product-type }


| Store | Store Product Type| IAP Supported |    
|---|---|---|
| Google Play Store| One-time, Subscriptions | CONSUMABLE, AUTO_SUBSCRIPTION |
| App Store| Consumable, Auto-Renewable | CONSUMABLE, AUTO_SUBSCRIPTION |
| ONE Store|	Managed product | CONSUMABLE|


<br>
<br>



> [Warning]  
> We shall not be liable for any damage or system error caused as a result of proceeding with payment with unspecified item type


<a id="consumable-subscription-product-consumableautorenewable"></a>
### Consumable Subscription Product (CONSUMABLEAUTORENEWABLE) { #consumable-subscription-product-consumableautorenewable }

<!-- TODO: translate body -->

<a id="inquiry-payment"></a>
## Inquiry payment { #inquiry-payment }

```
1. Click [Transaction] Tab.
2. Select [Store ID].
3. Select start date and end date in [Date].
4. Select sort option in [Sort]
5. Click [Search]  
```
![[]](http://static.toastoven.net/prod_iap/iap_transaction_list_en.png)


<br>
<br>

> [Reference]
> Payment Status   
>  - Reserved : ready to pay(If payment reservation request is complete but verification request is not received.)
>  - Success : completed successfully   
>  - Failure : failed (If an error occurs in payment verification process even though payment was attempted at store.) 
>  - Refund : refunded (If the admin manually refunded the payment in store.)



<a id="change-payment-status"></a>
## Change Payment Status { #change-payment-status }
```
You can change payment status in following conditions, 

1. If financial charge is successful, but IAP client does not receive receipt successfully, you should change payment status to 'Success'
   1.1 To change status to 'Success', currency and price on user's receipt will be needed.  

2. If user refunded payment at store, , you should change payment status to 'Refunded'
   2.1 After change, unconsumed payment API of Client will not return changed payment.

Payment which status will be changable shows [Modify] button right side as below. 

```
![[picture 6 Change payment status]](http://static.toastoven.net/prod_iap/iap_transaction_modify_en.png)

 
![[picture 7 Add additional information when changing statu]](http://static.toastoven.net/prod_iap/iap_transaction_update_success_en)


<a id="inquiry-payment-statistics"></a>
## Inquiry Payment Statistics { #inquiry-payment-statistics }

```
1. Click [Statistics]  
2. Select [currency]  
3. You may inquire ‘This month’s total gross’ and ‘Daily details’ using [<][>] button at store  
```

![[picture 6 Payment Statistics]](http://static.toastoven.net/prod_iap/iap_n_35.png)


