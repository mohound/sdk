# Mohound SDK
Download latest version: **0.1.7** [tar.gz](https://www.dropbox.com/s/dzwpzpj0kizgjhf/MohoundSDK-0.1.7.tar.gz) or
[zip](https://www.dropbox.com/s/sxan7bpes1eln37/MohoundSDK-0.1.7.zip)

## Installation
1. Download the SDK from any of the links provided at the top.
2. Untar the SDK (``tar -xvzf MohoundSDK-X.X.X.tar.gz``) and add the .a and the .h to the project
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
