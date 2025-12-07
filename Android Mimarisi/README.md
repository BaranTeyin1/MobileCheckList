# Linux Kernel
Linux Kernel, işletim sisteminin çekirdeğidir yani donanım ile yazılım arasında iletişimi kuran katmandır. 
- CPU, RAM, depolama, ekran, kamera, sensörler gibi tüm donanım bileşenlerini yönetir. Uygulamalar donanıma direkt erişemez, kernel aracılığıyla erişir.
- Her uygulamaya ne kadar RAM verileceğine karar verir, bellek izolasyonunu sağlar. Bir uygulamanın başka bir uygulamanın belleğine erişmesini engeller.
- Her uygulamayı kendi UID'si ile çalıştırır. Bu sayede uygulamalar birbirinden izole olur - Android'in sandbox yapısının temeli buradan gelir.

# HAL
Android, binlerce farklı cihazda çalışır. Framework standart bir API kullanır, HAL bunu cihaza özel komutlara çevirir.

# ART
ART, Android uygulamalarının çalıştırıldığı ortamdır. Java/Kotlin kodunun cihazda nasıl execute edileceğini yönetir. ART, Android uygulamalarının DEX bytecode'unu execute eder veya native koda derler (AOT/JIT).

# Android Framework
Android Framework, geliştiricilere hazır API'ler sunan, uygulamaların kullandığı üst düzey katmandır.

### Framework'ün Katmanları:
#### Application Framework (Java API):
- android.app (Activity, Service, Notification)
- android.content (Intent, ContentProvider, BroadcastReceiver)
- android.view (UI bileşenleri)
- android.os (Bundle, Handler, Looper)

#### System Services:
- PackageManagerService
- WindowManagerService
- LocationManager, NotificationManager vb.

### Components
#### Activity
- Kullanıcı arayüzü ekranları
- Her ekran bir Activity
- Örnek: LoginActivity, MainActivity, SettingsActivity

```xml
<activity android:name=".AdminActivity" 
          android:exported="true"/>
```

#### Service
- Arka planda çalışan işlemler
- Kullanıcı arayüzü yok
- Örnek: Müzik çalar, dosya indirme, senkronizasyon

```xml
<service android:name=".PaymentService"
         android:exported="true"/>
```

#### Broadcast Receiver
- Sistem veya uygulama eventlerini dinler
- Örnek: Telefon açıldı, şarj başladı, SMS geldi


```xml
<receiver android:name=".SmsReceiver"
          android:exported="true"/>
```

#### Content Provider
- Uygulamalar arası veri paylaşımı
- Veritabanı, dosya sistemi erişimi
- Örnek: Kişiler, medya dosyaları

```xml
<provider android:name=".UserDataProvider"
          android:exported="true"
          android:authorities="com.app.users"/>
```

### Intent Sistemi
Intent, component'ler arası iletişim mekanizması.

#### Explicit Intent:
```java
Intent intent = new Intent(this, TargetActivity.class);
startActivity(intent);
```

#### Implicit Intent:
```java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://example.com"));
startActivity(intent);
```

### Permission Sistemi:
- Normal Permissions: Otomatik verilir (internet)
- Dangerous Permissions: Kullanıcı onayı gerekir (kamera, konum, kişiler)

```xml
<uses-permission android:name="android.permission.CAMERA"/>
<uses-permission android:name="android.permission.READ_CONTACTS"/>
```

# Application Sandbox
Linux'ta her kullanıcının kendi UID'si vardır. Bir kullanıcı başka kullanıcının dosyalarını okuyamaz. Android'de Her uygulama, farklı bir Linux kullanıcısı olarak çalışır. Uygulama A, Uygulama B'nin dosyalarını göremez/okuyamaz çünkü farklı kullanıcılarda çalışıyorlar.

Uygulamalar bazen birbirleriyle iletişim kurmak zorunda. Android bunun için kontrollü mekanizmalar sunar:
- Intent Sistemi
- Content Provider
- Shared User ID (Aynı İmza)
