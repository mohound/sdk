# Mohound SDK
Download latest version: [**0.1.10**](https://www.dropbox.com/s/fnxhad9kgb9ovtf/MohoundSDK-0.1.10.zip)

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
