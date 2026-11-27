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

## Dört limit reseti — MASTER_PLAN ile uyumlu hedef, garanti değil
1. PHASE-00..03: teknik doğrulama, güvenli temel, finansal çekirdek, manuel işlemler.
2. PHASE-04..05: ödeme/recurrence ve finansal zekâ.
3. PHASE-06..07: şifreli yedek/restore/export, Android banka push.
4. PHASE-08..09: altı widget ve yerel release/quality.
PHASE-10 izinli SMS, PHASE-11 cloud backup, PHASE-12 CAS sync ayrı yetki ve kapasiteye bağlı; core local release blocker değil. iOS ayrı doğrulama/release lane. Gerçek veri PHASE-06 recovery gate sonrası.

Reset kapasitesi/son kullanma tarihleri kesin değil. Her reset sonunda çalışan checkpoint; doğrulanabilir dikey dilim, yarım özellik değil. Reset tüketmek amaç değil.

Her faz için ayrı, doğrudan Codex'e verilebilir goal prompt/blueprint hazırlanacak. Faz sayısı reset sayısına eşit olmak zorunda değil. [Codex yürütme protokolü](CODEX_EXECUTION_PROTOCOL.md): görev bağımlılıkları, doğrulama kapısı, ilerleme kontrolü ve kullanıcı onayı. Blueprint'ler hazır; [MASTER_PLAN](MASTER_PLAN.md) kesin faz dağılımı, [PROGRESS](PROGRESS.md) canlı durum, [START_HERE](START_HERE.md) başlangıç. Reset grupları tahmin; master plan ayrıntısı öncelikli.
