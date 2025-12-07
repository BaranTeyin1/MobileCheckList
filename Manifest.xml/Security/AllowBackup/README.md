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