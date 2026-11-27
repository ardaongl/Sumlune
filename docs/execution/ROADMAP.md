# Master roadmap

| Sıra | Aşama | Durum |
|---|---|---|
| 01 | Product Planning | Accepted kapsam |
| 02 | Design System | Accepted (ADR-0017; cihaz doğrulaması pending) |
| 03 | Technical Architecture | Accepted; stack koşullu, doğrulama Pending |
| 04 | Repository Initialization | Done; 42 Markdown baseline |
| 05 | Database & Financial Engine | Done (PLAN-02/03/04A/B tasarım) |
| 06 | Smart Capture Architecture | Done (tasarım; cihaz/izin pending) |
| 07 | Native Widget Architecture | Done (tasarım; renderer/cihaz pending) |
| 08 | Security & Cloud Sync | Done (tasarım; crypto/provider/cihaz pending) |
| 09 | Screen Specifications | Done (PLAN-08 tasarım) |
| 10 | Testing & Quality Strategy | Done (ADR-0018; testler henüz Not run) |
| 11 | Codex Integration Plan | Done (ADR-0019, 13 blueprint, progress) |
| 12 | Implementation | Açık onaya kadar yasak |

## Dört limit reseti — önerilen hedef, garanti değil
1. Core Finance: bootstrap + spike, temel UI, DB/engine, hesap/işlem/şablon, TR/EN; ilk çalışan Android build hedefi.
2. Financial Planning: abonelik, taksit, borç, ödeme, recurrence, takvim, bildirim.
3. Smart Finance: Android capture, otomasyon, bütçe, analitik, tahmin, birikim; kritik widget erken teslim değerlendirilecek.
4. Native Experience & Quality: altı widget, güvenlik, backup/export, test, performans, Android APK/iOS build hazırlığı. Widget/capture spike ilk reset; güvenlik temelleri baştan. Bulut backup ve CAS sync ayrı ardışık opsiyonel geliştirme fazları; core release blocker değil (ADR-0016).

Reset kapasitesi/son kullanma tarihleri kesin değil. Her reset sonunda çalışan checkpoint; doğrulanabilir dikey dilim, yarım özellik değil. Reset tüketmek amaç değil.

Her faz için ayrı, doğrudan Codex'e verilebilir goal prompt/blueprint hazırlanacak. Faz sayısı reset sayısına eşit olmak zorunda değil. [Codex yürütme protokolü](CODEX_EXECUTION_PROTOCOL.md): görev bağımlılıkları, doğrulama kapısı, ilerleme kontrolü ve kullanıcı onayı. Blueprint'ler hazır; [MASTER_PLAN](MASTER_PLAN.md) kesin faz dağılımı, [PROGRESS](PROGRESS.md) canlı durum, [START_HERE](START_HERE.md) başlangıç. Reset grupları tahmin; master plan ayrıntısı öncelikli.
