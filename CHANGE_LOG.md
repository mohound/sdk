# Change Log

## 0.1.11

* Add support for custom event tracking. It represents what the user is supposed
  to do within the app, will be used to make marketing decisions. Incorporate
  them, by doing:

    ```objc
    [MohoundSDK trackEvent:@"EventName"];
    ```

* Improves error handling.

## 0.1.10

* Add support for arm64 architecure

## 0.1.9

* Full integration with Facebook
* Fixes problem when reporting installations to CPI networks

## 0.1.8

* SDK can be used now with the simulator (the server now responds to simulator
  calls)
* SDK library renamed to MohoundSDK (from MoHoundSDK), in order to reflect our
  company name, so, you will need to rename any MoHound instance to **Mohound**
* The SDK is now distributed as a framework, make sure to do the following
  change:

    ```objc
    // Older versions:
    #import "MoHoundSDK.h"

    // New version:
    #import <MohoundSDK/MohoundSDK.h>
    ```

## 0.1.7

* Remove UDID support
* Improve support for CPI networks

## 0.1.6

* Jailbroken in-app purchases detection

## 0.1.5

* CPI support

## 0.1.4

* Added activation tracking
* Added purchase for non in-app events

## 0.1.3

* To increase accuracy changed the in app purchase tracking method signature to:

    ```objc
    - (NSDictionary *)getPurchaseParams:(SKPaymentTransaction *)transaction;
    ```

## 0.1.2

* Change the init method signature to:

    ```objc
    + (void)initWithAppKey:(NSString *)appKey andSecret:(NSString *)appSecret;
    ```

* Bug fix with params on in-app purchases
* Fingerprinting improvements
