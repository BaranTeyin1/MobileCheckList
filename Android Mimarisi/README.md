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
#### Application Framework (Java API): Geliştiricilerin kullandığı public API'ler:
- android.app (Activity, Service, Notification)
- android.content (Intent, ContentProvider, BroadcastReceiver)
- android.view (UI bileşenleri)
- android.os (Bundle, Handler, Looper)

#### System Services: Arka planda çalışan servisler:
- ActivityManagerService: Uygulama yaşam döngüsü
- PackageManagerService: APK kurulum/kaldırma 
- WindowManagerService: Ekran yönetimi
- LocationManager, NotificationManager vb.