# Risk ve açık konular

| ID | Risk / bilinmeyen | Azaltma |
|---|---|---|
| R-01 | Repo ilk kurulum engeli giderildi; görünürlük public | Yazma doğrulandı; ürün sahibi private yapabilir |
| R-02 | Expo/SQLCipher/Drizzle ve integer bridge | SDK/cihaz spike, money ADR |
| R-03 | Background capture OS sınırlaması | Durable queue, resume, force-stop/reboot test |
| R-04 | SMS izni/Play policy | Güncel policy ve kurulum testi, flag, manuel fallback |
| R-05 | Widget SDK/platform farkı | WidgetKit/Glance spike, Expo Widgets paritesi varsayılmaz |
| R-06 | Biometrik kilit vs background key erişimi | Threat model, security ADR |
| R-07 | Çift kayıt/yanlış parser | Maskeli fixture, idempotency, uncertain review |
| R-08 | Kur/recurrence/taksit rounding | Finansal motor ADR ve property tests |
| R-09 | Bulut E2EE/conflict | Protokol, key recovery, aggregate atomicity |
| R-10 | Dört reset kapasitesi bilinmiyor | Dikey dilim, checkpoint, öncelik |
| R-11 | iOS signing/cihaz/dağıtım | Build hedefleri test; garanti yok |
| R-12 | Widget privacy/stale snapshot | Maskeli snapshot, invalidation, OS refresh sınırları |
| R-13 | Banka formatları bilinmiyor | Öncelikli bankalar, sentetik fixture |

Riskler teknik taslaktır; cihaz doğrulaması yok.
