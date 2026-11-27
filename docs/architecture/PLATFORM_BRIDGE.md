# Native bridge — Proposed

Expo development build ve Expo Modules API, Kotlin Android/Swift iOS. Expo Go yeterli değil. Ortak capability contract; dağınık platform kontrolleri yok. Native ledger'a doğrudan yazmaz.

Android capture ADR-0014: NotificationListenerService, gated RECEIVE_SMS receiver, şifreli structured queue ve foreground drain; WorkManager/Headless JS yalnız ihtiyaç ve spike sonrası. Keystore; widget renderer ADR-0015 koşullu platform seçimi. iOS: WidgetKit/SwiftUI, App Groups, App Intents, Keychain, OS izinli background tasks; banka SMS/bildirim capture yok. Native target, manifest/config plugin gerçek cihazda test; prebuild özel target/servis kaybetmemeli.

Port adayları: PlatformCapabilities, CaptureSource, CaptureQueue, WidgetPublisher, NotificationScheduler, SecureKeyStore. Sözleşmede versiyon, timestamp, doğrulanmış para temsili, hata tipleri. Arka plan/hatırlatma teslimi garanti değil; recovery/resume.

Spike: Android app kapalı/force-stop/reboot/izin iptali, iOS extension build/deep link, SQLCipher key koşulları. Test olmadan production desteği ilan etme.

Widget için ortak versioned snapshot publisher, renderer adapter ve deep-link/auth gate [WIDGETS](WIDGETS.md) içinde Accepted (ADR-0015). Expo Widgets sürüm/özellik desteği cihazda doğrulanır; gerekirse Glance ve WidgetKit. Native widget finansal DB/key kullanmaz.
