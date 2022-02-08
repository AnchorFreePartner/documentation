# Configuration

### Proguard Rules

Proguard rules are included in sdk, but you can use these if required:

```
    -dontwarn okio.**
    -keepattributes InnerClasses
    -dontwarn sun.misc.**
    -dontwarn java.lang.invoke.**
    -dontwarn okhttp3.**
    -dontwarn com.anchorfree.sdk.**
    -dontwarn okio.**
    -dontwarn javax.annotation.**
    -dontwarn org.conscrypt.**
    -keepnames class okhttp3.internal.publicsuffix.PublicSuffixDatabase
    #DNSJava
    -keep class org.xbill.DNS.** {*;}
    -dontnote org.xbill.DNS.spi.DNSJavaNameServiceDescriptor
    -dontwarn org.xbill.DNS.spi.DNSJavaNameServiceDescriptor
    -keep class * implements com.google.gson.TypeAdapterFactory
    -keep class * implements com.google.gson.JsonSerializer
    -keep class * implements com.google.gson.JsonDeserializer
    -keep class com.anchorfree.sdk.SessionConfig { *; }
    -keep class com.anchorfree.sdk.fireshield.** { *; }
    -keep class com.anchorfree.sdk.dns.** { *; }
    -keep class com.anchorfree.sdk.HydraSDKConfig { *; }
    -keep class com.anchorfree.partner.api.ClientInfo { *; }
    -keep class com.anchorfree.sdk.NotificationConfig { *; }
    -keep class com.anchorfree.sdk.NotificationConfig$Builder { *; }
    -keep class com.anchorfree.sdk.NotificationConfig$StateNotification { *; }
    -keepclassmembers public class com.anchorfree.ucr.transport.DefaultTrackerTransport {
       public <init>(...);
     }
     -keepclassmembers class com.anchorfree.ucr.SharedPrefsStorageProvider{
        public <init>(...);
     }
     -keepclassmembers class com.anchorfree.sdk.InternalReporting$InternalTrackingTransport{
     public <init>(...);
     }
     -keep class com.anchorfree.sdk.exceptions.* {
        *;
     }
      
    -keepclassmembers class * implements javax.net.ssl.SSLSocketFactory {
        final javax.net.ssl.SSLSocketFactory delegate;
    }
    
    # https://stackoverflow.com/questions/56142150/fatal-exception-java-lang-nullpointerexception-in-release-build
    -keepclassmembers,allowobfuscation class * {
      @com.google.gson.annotations.SerializedName <fields>;
    }
```

### Set VPN process name

Add this string resource to your source file to set custom process name for vpn

```
<string name="vpn_process_name" translatable="false">:vpn</string>
```

### Java 8

Add Java 8 support to project **build.gradle**

```
compileOptions {
    sourceCompatibility 1.8
    targetCompatibility 1.8
}
```

If you cannot enable java 8 support in your project, please contact us for further details.

### Notifications

To configure sdk notification, use **NotificationConfig.Builder** class

**Disable notifications**

```
    NotificationConfig.Builder builder = NotificationConfig.newBuilder();
    builder = builder.disabled()
```

**Notifications for different states**

```
//Notification to be displayed when vpn is connected
builder.inConnected("Title","Message");
//Notification to be displayed when vpn is not connected
builder.inIdle("Title","Message");
//Notification to be displayed when vpn is connecting
builder.inConnecting("Title","Message");
//Notification to be displayed when vpn is paused(waiting for network connection)
builder.inPause("Title","Message");
//Notification to be displayed if Client Network List feature is used
builder.inCnl("Title","Message");
```

**Notification message and title fallback**

By default, sdk displays notification for state CONNECTED and PAUSED.

If **inConnected** was not called, it tries to use value set with **title** message

If `NotificationConfig.Builder.title` was not set, it will use App name as in launcher

If **inConnected** was not called, it will try to use string resource **default\_notification\_connected\_message**

If **inPause** was not called, it will try to use string resource **default\_notification\_paused\_message**

#### Notification click intent

To configure action when a user clicks a notification, use **clickAction** method. You must have Activity responding to the specified action. Action will be used to create an Intent. If **clickAction** is not specified, sdk will open application launch activity on notification click.

In intent extras sdk will set a boolean value **UnifiedSDKNotificationManager.EXTRA\_NOTIFICATION** as **true**.

To handle click action, register `intent-filter` with your activity

```
<intent-filter>
    <action android:name="com.sdk.notification.action"/>
    <category android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```

#### Update notification preferences

Notification config can be updated calling the sdk method

```
    UnifiedSDK.update(createNotificationConfig());
```

##
