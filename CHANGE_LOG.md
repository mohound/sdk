## 0.1.6
* Jailbroken in-app purchases detection

## 0.1.5
* CPI Support

## 0.1.4
* Added activation tracking
* Added purchase for non in-app events

## 0.1.3
* To increase accuracy changed the in app purchase tracking method signature to:
-(NSDictionary *) getPurchaseParams:(SKPaymentTransaction *)transaction;

## 0.1.2
* Change the init method signature to + (void)initWithAppKey:(NSString *)appKey andSecret:(NSString *)appSecret;
* Bug fix with params on in-app purchases
* Fingerprinting improvements
