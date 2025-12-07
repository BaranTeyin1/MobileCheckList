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

# android:usesCleartextTraffic Nedir?
uygulamanın şifrelenmemiş HTTP trafiğine izin verip vermediğini belirleyen bir flag'tir.

Eğer usesCleartextTraffic="true" ise saldırgan, kullanıcı ile sunucu arasına girerek mitm saldırısı gerçekleştirebilir.
