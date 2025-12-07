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