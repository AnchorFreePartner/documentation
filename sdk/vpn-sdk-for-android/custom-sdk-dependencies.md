# Custom sdk dependencies



You can control some parts of sdk internal logic by overriding dependencies used by sdk.

1. Define raw resource e.g **sdk\_deps.json**
2. Setup meta-data in **AndroidManifest.json**

   ```markup
   <meta-data
            android:name="com.anchorfree.vpnsdk.deps"
            android:resource="@raw/sdk_deps"/>
   ```

3. Ensure custom dependency classes is not renamed or removed by ProGuard or similar software

Content of **sdk\_deps.json**

General structure of dependencies config looks like

```javascript
{
  "dependency 1 key": {
    "type": "class 1 name for dependency to use"
  },
  "dependency 2 key": {
    "type": "class 2 name for dependency to use"
  }
}
```

### Possible dependencies overrides

#### Custom logger

1. Define class that extends **com.anchorfree.vpnsdk.UnifiedLogDelegate**

```java
@Keep
public class CustomLogger extends UnifiedLogDelegate {
    @Override
    public void log(final int priority, Throwable throwable, String tag, String format, Object... args) {

    }

    @Override
    public void setLogLevel(final int logLevel) {

    }
}
```

Setup SDK dependency override in **sdk\_deps**

```javascript
 {
     "logger": {
        "type": "com.sdk.sample.CustomLogger"
     }
 }
```

#### Additional configuration of OkHttpClient used in sdk

1. Define class that implements **OkHttpNetworkLayer.HttpClientConfigurer**

```java
@Keep
public class SampleOkHttpConfigurer implements OkHttpNetworkLayer.HttpClientConfigurer {
    @Override
    public void configure(@NonNull final OkHttpClient.Builder builder) {
        //perform custom configuration of OkHttpClient.Builder
    }
}
```

1. Setup SDK dependency override in **sdk\_deps**

```javascript
 {
     "okHttpConfigurer": {
        "type": "com.sdk.sample.SampleOkHttpConfigurer"
     }
 }
```

#### Custom backend URL rotator

1. Define class that implements **UrlRotator**

```java
public class SampleUrlRotator implements UrlRotator {
    @Override
    public void failure(String httpUrl, PartnerRequestException error) {
        //mark url as failed
    }

    @Override
    public void success(String httpUrl) {
        //mark url as success
    }

    @Override
    public String provide() {
        // return url for backend calls
        return null;
    }

    @Override
    public int size() {
        // return number of possible urls for rotation
        return 1;
    }
}
```

Define class that implements **UrlRotatorFactory**

```java
@Keep
public class SampleUrlRotatorFactory implements UrlRotatorFactory {
    @Override
    public BackendUrlRotator create(Context context, ClientInfo clientInfo) {
        return new SampleUrlRotator();
    }
}
```

Setup SDK dependency override in **sdk\_deps**

```javascript
 {
     "urlRotator": {
        "type": "com.sdk.sample.SampleUrlRotatorFactory"
     }
 }
```

