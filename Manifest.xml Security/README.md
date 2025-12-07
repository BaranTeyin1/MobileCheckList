# AndroidManifest.xml Nedir?
AndroidManifest.xml, Android sistemine uygulama hakkında bilgi verir:

## 1.
```xml
<manifest package="com.example.myapp"
          android:versionCode="1"
          android:versionName="1.0">
```

- package: Uygulamanın benzersiz ID'si.

## 2. Component Tanımları
Uygulamadaki tüm component'leri burada bildirmen gerekir:
```xml
<application>
    <!-- Activity'ler -->
    <activity android:name=".MainActivity"/>
    <activity android:name=".LoginActivity"/>
    
    <!-- Service'ler -->
    <service android:name=".MusicService"/>
    
    <!-- Broadcast Receiver'lar -->
    <receiver android:name=".BootReceiver"/>
    
    <!-- Content Provider'lar -->
    <provider android:name=".UserDataProvider"/>
</application>
```

## 3. İzin Talepleri
Uygulama hangi izinlere ihtiyaç duyuyorsa burada belirtilir:
```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.CAMERA"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

Kullanıcı bu izinleri onaylamazsa uygulama bu özelliklere erişemez.

## 4. Uygulama Ayarları
```xml
<application
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/AppTheme"
    android:debuggable="false"
    android:allowBackup="false">
```

- debuggable: Debug modu
- allowBackup: Backup izni

## 5. Intent Filter'lar
Hangi intent'leri dinlediğini belirtir:
```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
</activity>
```

## 6. Donanım/Yazılım Gereksinimleri
```xml
<uses-feature android:name="android.hardware.camera" android:required="true"/>
<uses-sdk android:minSdkVersion="23" android:targetSdkVersion="33"/>
```

- uses-feature: Kamera, GPS gibi donanım gereksinimi
- uses-sdk: Minimum ve hedef Android versiyonu

# APKTool ile Manifest Decode
APKTool, binary XML'i tekrar readable XML'e çevirir:
```bash
apktool d app.apk -o decoded/
```

