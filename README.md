# Mohound SDK

Download latest version: [**0.1.11**](https://www.dropbox.com/s/r4si4t8i1g21wj7/MohoundSDK-0.1.11.zip)

## Installation

1. Download and unzip the SDK.
2. Add the whole MohoundSDK.framework folder to the project.
3. Be sure to have the **AdSupport** and **StoreKit** frameworks in your project (Build phases -> Link Binary With 
Libraries). If your deployment target is iOS 5.1 or less, make sure to set AdSupport as **Optional**.
4. Go to **Build Settings** and under **Linking** find **Other Linker Flags** and add ``-ObjC``.
5. ``#import <MohoundSDK/MohoundSDK.h>`` in every file where the SDK will be called.
6. In your app's ``application:didFinishLaunchingWithOptions:`` add the following line replacing KEY and SECRET with
   your info:  

```objc    
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MohoundSDK initWithAppKey:@"<#KEY#>" andSecret:@"<#SECRET#>"];
  ...
}
```

## Testing connectivity

To check connectivity to the backend you can add the following lines right after the initWithAppKey method but **remember 
to delete them** before releasing your app!:

```objc 
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MohoundSDK initWithAppKey:@"<#KEY#>" andSecret:@"<#SECRET#>"];
  [MohoundSDK setDebugMode:true];
  [MohoundSDK ping];
  ...
}
```

This should give you a Pong from the server showing that everything is working.

## Usage

### Purchases

In case you want to run some ROI campaigns, then you'll need to track purchases. We support both in-app or outside your
app, you'll need just to add the following pieces of code to make it work.

#### In-app purchases

* First, register your products with our SDK, right inside the
   `productsRequest:didReceiveResponse:` method:

      ```ojbc
     - (void)productsRequest:(SKProductsRequest *)request didReceiveResponse:(SKProductsResponse *)response
      {
        ...
        [MohoundSDK registerProducts:response.products];
        ...
      }
      ```

* Then, call `[MohoundSDK trackPurchase:]`, with an `SKPaymentTransaction`
   when a purchase gets completed:

      ```objc
      [MohoundSDK trackPurchase:transaction];
      ```

#### Out-app purchases

You'll just need to call `[MohoundSDK trackPurchaseWithUSDValue:forItem]` 
when your transaction gets completed.

For example, if you want to track the purchase of a Diet Coke six pack, do:

```objc
[Mohound trackPurchaseWithUSDValue:[NSNumber numberWithFloat:2.99] forItem:@"Diet Coke six pack"];
```

### Events

An event is a valuable action for an app. It represents what the user is
supposed to do within the app. It will be used to make marketing decisions.
i.e. it can be a user giving a review, signing up, or inviting a friend to use
an app.

For example, if you want to track when a user invited a friend, do:

```objc
[MohoundSDK trackEvent:@"UserInvitation"];
```
