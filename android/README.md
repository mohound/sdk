# Mohound Android SDK
Download latest version: [**0.1.1**](https://www.dropbox.com/s/3nyihzig426eiq7/mohound-0.1.1.jar)

## Installation
1. Download and unzip the SDK
2. Copy the .jar file inside the `libs` directory of your Android project

**NOTE** If your project does not have a lib directory, place the .jar file in
another directory and add the directory to your Java CLASSPATH variable.

## Integration

### `AndroidManifest.xml`

1. You will need to add the following permissions:

    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    ```

2. Add Mohound referrer receiver inside your `application` tag:

   	```xml
   	<receiver android:exported="true" android:name="com.mohound.sdk.ReferrerReceiver">
   	  <intent-filter>
        <action android:name="com.android.vending.INSTALL_REFERRER"></action>
      </intent-filter>
    </receiver>
   	```

3. Add Mohound settings meta data tags inside your `application` tag, replace
   `APP_KEY` and `SECRET_KEY` with your keys:

	```xml
  <meta-data android:name="MohoundAppKey" android:value="APP_KEY" />
  <meta-data android:name="MohoundAppSecret" android:value="SECRET_KEY" />
	```

4. If you want to enable debug mode (prints verbosely to Logger), add the
   following meta data tag:

   	```xml
    <meta-data android:name="MohoundDebugMode" android:value="true" />
   	```

The following is an example of an `AndroidManifest.xml` properly integrated:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.mohound.DemoApp"
    android:versionCode="1"
    android:versionName="1.0" >

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >

        <meta-data android:name="MohoundAppKey"
            android:value="APP_KEY" />
        <meta-data android:name="MohoundAppSecret"
            android:value="APP_SECRET" />

        <receiver
            android:exported="true"
            android:name="com.mohound.sdk.ReferrerReceiver">
      		<intent-filter>
            	<action android:name="com.android.vending.INSTALL_REFERRER" />
      		</intent-filter>
		</receiver>

        <activity
            android:name="com.mohound.DemoApp.MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

### Calling Mohound methods

1. Add an `import com.mohound.sdk.Mohound;` on each file where the SDK will be
   called.
2. Call `Mohound.onCreate(activity)` when your main `Activity` gets created:

    ```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Mohound.onCreate(this);
        ...
    }
    ```

## Testing connectivity

To check connectivity to the backend you can add the following line in your
`onCreate` method, and enable **MohoundDebugMode** but **remember to delete
them** before releasing your app!:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Mohound.onCreate(this);
    Mohound.ping();
    ...
}
```

This should give you a Pong from the server showing that everything is working.

## Usage

### Purchases

In case you want to run some ROI campaigns, then you'll need to track purchases. You'll need just to add the following
pieces of code to make it work.

When your purhcase was success, call `Mohound.trackPurchase(value, item)`. For example, we want to track a 1.50 USD
purchase of 5 tokens, then use:

```java
Mohound.trackPurchase(1.5, "5 tokens");
```

**NOTE** Value should be the `double` or `float` **USD** amount of the purchase. Item is a reference to the purchased
object.

### Events

An event is a valuable action for an app. It represents what the user is supposed to do within the app. It will be used to make marketing decisions. i.e. it can be a user giving a review, signing up, or inviting a friend to use an app.

For example, if you want to track when a user invited a friend, do:

```java
Mohound.trackEvent("UserInvitation");
```
