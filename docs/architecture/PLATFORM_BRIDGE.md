# Native bridge — Proposed

Expo development build ve Expo Modules API, Kotlin Android/Swift iOS. Expo Go yeterli değil. Ortak capability contract; dağınık platform kontrolleri yok. Native ledger'a doğrudan yazmaz.

Android: NotificationListenerService, izinli SMS Receiver, güvenli kalıcı queue, WorkManager, gerekirse Headless JS, Glance, Keystore. iOS: WidgetKit/SwiftUI, App Groups, App Intents, Keychain, OS izinli background tasks; banka SMS/bildirim capture yok. Native target, manifest/config plugin gerçek cihazda test; prebuild özel target/servis kaybetmemeli.

Port adayları: PlatformCapabilities, CaptureSource, CaptureQueue, WidgetPublisher, NotificationScheduler, SecureKeyStore. Sözleşmede versiyon, timestamp, doğrulanmış para temsili, hata tipleri. Arka plan/hatırlatma teslimi garanti değil; recovery/resume.

Spike: Android app kapalı/force-stop/reboot/izin iptali, iOS extension build/deep link, SQLCipher key koşulları. Test olmadan production desteği ilan etme.
