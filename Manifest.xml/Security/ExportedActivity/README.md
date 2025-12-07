# Exported Activity Nedir?
Exported Activity, başka uygulamalar tarafından başlatılabilen bir ekrandır. Aşağıdaki durumlarda activity exported olur.

Android 11 ve altı:
```xml
<activity android:name=".ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
    </intent-filter>
</activity>
<!-- Intent filter var = otomatik exported="true" -->
```

Android 12+ (API 31+):
```xml
<activity 
    android:name=".ShareActivity"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
    </intent-filter>
</activity>
```

