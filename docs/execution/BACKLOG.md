# Backlog — planlama

| ID | Görev | Bağımlılık | Durum |
|---|---|---|---|
| PLAN-00 | Repo erişimi ve doküman baseline commit | GitHub yazma | Done |
| PLAN-01 | Mimari önerileri gözden geçir/onayla | Baseline | Done |
| PLAN-02 | Finansal invariants, money representation, hesap modeli | PLAN-01 | Done |
| PLAN-03 | ERD, kolon, constraint, index, migration ve kesin FX/rounding/wire | PLAN-02 | Done (tasarım; DEV-00 doğrulaması pending) |
| PLAN-04 | Payment & Recurrence (04A) + Financial Intelligence (04B) | PLAN-03 | Done (04A/04B tasarım Accepted) |
| PLAN-05 | Capture parser, bankalar, dedup, queue, otomasyon | PLAN-04 | Done (tasarım Accepted; banka/izin doğrulaması pending) |
| PLAN-06 | Widget snapshot/deep link sözleşmesi | PLAN-04/05 | Done (tasarım Accepted; renderer/cihaz pending) |
| PLAN-07 | Security, backup, cloud sync | PLAN-03/05/06 | Done (tasarım Accepted; doğrulama pending) |
| PLAN-08 | Ekran, design system ve kabul kriterleri | PLAN-02..07 | Done (tasarım Accepted; UI/device pending) |
| PLAN-09 | 09A Testing & Quality, 09B faz başına ayrıntılı Markdown goal prompt/blueprint, progress kontrol ve Codex handoff | PLAN-01..08 | Done (ADR-0018/0019; blueprint ve progress hazır) |
| DEV-00 | SDK uyumu ve native/SQLCipher spike | Açık kodlama onayı | Not authorized |
| DEV-01 | PHASE-01..12 implementation (00–09 local; 10 SMS, 11–12 cloud ayrı) | DEV-00 + plan | Not authorized |

PLAN-03 çekirdek şema ve FX/rounding/wire tamamlandı. PLAN-04A/B tamamlandı; PLAN-05 tamamlandı; PLAN-06 tamamlandı; PLAN-07 tamamlandı; PLAN-08 tamamlandı; PLAN-09A/B tamamlandı; implementation [MASTER_PLAN](MASTER_PLAN.md), [PROGRESS](PROGRESS.md) üzerinden izlenir. PHASE-00 ayrı kullanıcı izni bekler. Koşullu stack doğrulaması DEV-00 kapsamındadır. Bu görevler uygulama kodlama izni değildir.
