# android:allowBackup Nedir?android:allowBackup
Uygulamanın verilerinin ADB ile yedeklenip yedeklenemeyeceğini belirleyen bir flag'tir.

Android, kullanıcıların uygulama verilerini yedeklemesine izin verir:
### 1. ADB Backup
Bilgisayardan ADB komutu ile:
```bash
bashadb backup -f backup.ab -noapk com.example.app
```

#### Ne yedeklenir?
/data/data/com.example.app/ klasörünün içindekiler:
- databases/ → SQLite veritabanları
- shared_prefs/ → SharedPreferences (XML dosyaları)
- files/ → Internal storage dosyaları
- cache/ → Cache dosyaları


#### Ne yedeklenmez?
- APK dosyası (-noapk parametresi)
- External storage (/sdcard/)
- Native kütüphaneler

### 2. Google Backup
Android 6.0+ cihazlarda otomatik:
- Google Drive'a yedeklenir
- Cihaz değiştiğinde otomatik restore
- Kullanıcı ayarlardan kapatabilir

# Network Security Config
Manifest'te Tanımlama
```xml
<application android:networkSecurityConfig="@xml/network_security_config">
```
Config Dosyası Yapısı
res/xml/network_security_config.xml:
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <!-- Base config (tüm domain'ler için) -->
    <base-config cleartextTrafficPermitted="false">
        <trust-anchors>
            <certificates src="system"/>
        </trust-anchors>
    </base-config>
    
    <!-- Domain-specific config -->
    <domain-config cleartextTrafficPermitted="false">
        <domain includeSubdomains="true">api.example.com</domain>
        <pin-set expiration="2025-12-31">
            <pin digest="SHA-256">base64encodedpin==</pin>
            <pin digest="SHA-256">backuppin==</pin>
        </pin-set>
    </domain-config>
    
    <!-- Debug-only config -->
    <debug-overrides>
        <trust-anchors>
            <certificates src="user"/>
        </trust-anchors>
    </debug-overrides>
</network-security-config>
```

## android:usesCleartextTraffic Nedir?
uygulamanın şifrelenmemiş HTTP trafiğine izin verip vermediğini belirleyen bir flag'tir.

Eğer usesCleartextTraffic="true" ise saldırgan, kullanıcı ile sunucu arasına girerek mitm saldırısı gerçekleştirebilir.

# android:debuggable Nedir?
Eğer production uygulamada android:debuggable="true" kalırsa saldırgan uygulamaya debugger bağlayabilir:
```bash
adb forward tcp:8000 jdwp:$(adb shell ps | grep com.example.app | awk '{print $2}')
jdb -attach localhost:8000
```

- Değişkenleri okuyabilir
- Değişkenleri değiştirebilir

Frida, runtime'da kod enjekte etme aracı. Debuggable uygulamalarda çok kolay çalışır.

Debuggable uygulamanın belleğini dump alabilirsin:
```bash
adb shell "cat /proc/[PID]/maps"
adb shell "dd if=/proc/[PID]/mem of=/sdcard/dump.bin"
adb pull /sdcard/dump.bin
```

Debuggable uygulamalarda root olmadan uygulama verilerine erişebilirsin.

Debuggable uygulamalar allowBackup="false" olsa bile backup alınabilir.

# Exported Activity Nedir?
Exported Activity, başka uygulamalar tarafından başlatılabilen bir ekrandır. Aşağıdaki durumlarda activity exported olur.

Android 11:
```xml
<activity android:name=".ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
    </intent-filter>
</activity>
```

Android 12+:
```xml
<activity android:name=".ShareActivity" android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
    </intent-filter>
</activity>
```

