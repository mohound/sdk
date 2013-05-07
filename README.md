# Mohound SDK
Download latest version: [**0.1.8**](https://www.dropbox.com/s/oji1q8e3zkojyfz/MohoundSDK-0.1.8.zip)

## Installation
1. Download and unzip the SDK.
2. Add the whole MohoundSDK.framework folder to the project.
3. Be sure to have the **AdSupport** and **StoreKit** frameworks in your project (Build phases -> Link Binary With 
Libraries).
4. ``#import <MohoundSDK/MohoundSDK.h>`` in every file where the SDK will be called.
5. In your app's ``application:didFinishLaunchingWithOptions:`` add the following line replacing KEY and SECRET with
   your info:  

```objc    
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MohoundSDK initWithAppKey:@"KEY" andSecret:@"SECRET"];
  ...
}
```

## Testing connectivity
To check connectivity to the backend you can add the following lines right after the initWithAppKey method but **remember 
to delete them** before releasing your app!:

```objc 
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  [MohoundSDK initWithAppKey:@"KEY" andSecret:@"SECRET"];
  [MohoundSDK setDebugMode:true];
  [MohoundSDK ping];
  ...
}
```

This should give you a Pong from the server showing that everything is working.
