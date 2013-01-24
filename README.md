# Mohound SDK
Download latest version: **0.1.4** [tar.gz](https://www.dropbox.com/s/v6xyrxtwkuy2lj8/MohoundSDK-0.1.4.tar.gz) or
[zip](https://www.dropbox.com/s/qxse7v45nqte7dj/MohoundSDK-0.1.4.zip)

## Installation
1. Download the SDK from [here.](https://www.dropbox.com/s/v6xyrxtwkuy2lj8/MohoundSDK-0.1.4.tar.gz)
2. Untar the SDK and add the .a and the .h to the project
3. Be sure to have the **AdSupport** and **StoreKit** frameworks in your project (Build phases -> Link Binary With 
Libraries).
4. ``#import "MoHoundSDK.h"`` in every file where the SDK will be called.
5. In your app's ``application:didFinishLaunchingWithOptions:`` add the following line replacing KEY and SECRET with
   your info:  

```objc    
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MoHoundSDK initWithAppKey:@"KEY" andSecret:@"SECRET"];
  ...
}
```

## Testing connectivity
To check connectivity to the backend you can add the following lines right after the initWithAppKey method but **remember 
to delete them** before releasing your app!:

```objc 
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MoHoundSDK initWithAppKey:@"KEY" andSecret:@"SECRET"];
  [MoHoundSDK setDebugMode:true];
  [MoHoundSDK ping];
  ...
}
```

This should give you a Pong from the server showing that everything is working.

## Tracking in-app purchases
If you own a game or have a free to download app and profit from user getting in-app content, follow this steps to get 
the tracking working properly:

### 1. Register the available items.
Once you get the products responses from apple on the ``didReceiveResponse`` method, register the products with:

```objc
- (void)productsRequest:(SKProductsRequest *)request didReceiveResponse:(SKProductsResponse *)response
{
    [MoHoundSDK registerProducts:response.products];
    ...
}
```

### 2. Register the purchase.
When a user actually purchse a product send the transaction to Mohound like this:

```objc
- (void)paymentQueue:(SKPaymentQueue *)queue updatedTransactions:(NSArray *)transactions
{
    for (SKPaymentTransaction *transaction in transactions) {
        switch (transaction.transactionState) {
            case SKPaymentTransactionStatePurchased:
                [MoHoundSDK trackPurchase:transaction];
                ...
                break;
            ...
        }
    }
}
```

## Tracking activations
An activation is a valuable action for an app. It represents what the user is supposed to do within the app. Activations 
will be used to make marketing decisions and might be actions like sharing something, writing a review or inviting a 
friend.

You can track several actions but we strongly advise to just track the most important one. 

Activations can have values that are relative to each other. If you are tracking only one activation
we recommend using 1 for the value.

To track an activation use the following SDK method.

```objc
[MoHoundSDK trackActivation:[NSNumber numberWithFloat:1.0]];
```

## Tracking out-app purchases
If you need to track a purchase event that is not linked to an in-app purchase but to an out-app purchase, like someone 
asking for a real-world delivery, you can track those events using the following call.

**IMPORTANT: The value should be in USD**

```objc
[MoHoundSDK trackPurchaseWithUSDValue:[NSNumber numberWithFloat:19.99] forItem:@"Diet coke pack."];
```
