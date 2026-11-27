# Backlog — planlama

| ID | Görev | Bağımlılık | Durum |
|---|---|---|---|
| PLAN-00 | Repo erişimi ve doküman baseline commit | GitHub yazma | Done |
| PLAN-01 | Mimari önerileri gözden geçir/onayla | Baseline | Done |
| PLAN-02 | Finansal invariants, money representation, hesap modeli | PLAN-01 | Done |
| PLAN-03 | ERD, kolon, constraint, index, migration ve kesin FX/rounding/wire | PLAN-02 | Done (tasarım; DEV-00 doğrulaması pending) |
| PLAN-04 | Recurrence, kart, taksit, debt, forecast politikaları | PLAN-03 | In progress (ödeme taslağı Proposed) |
| PLAN-05 | Capture parser, bankalar, dedup, queue, otomasyon | PLAN-02 | Pending |
| PLAN-06 | Widget snapshot/deep link sözleşmesi | PLAN-02 | Pending |
| PLAN-07 | Security, backup, cloud sync | PLAN-03/05/06 | Pending |
| PLAN-08 | Ekran ve kabul kriterleri | PLAN-02/04 | Pending |
| PLAN-09 | Test planı, görev bağımlılıkları, faz başına ayrıntılı Markdown goal prompt/blueprint, ilerleme kontrolü ve Codex handoff | PLAN-01..08 | Pending |
| DEV-00 | SDK uyumu ve native/SQLCipher spike | Açık kodlama onayı | Not authorized |
| DEV-01 | Dört reset implementation | DEV-00 + plan | Not authorized |

PLAN-03 çekirdek şema ve FX/rounding/wire tamamlandı. PLAN-04 ortak ödeme motoru detayları aktif; ardından Financial Intelligence. Koşullu stack doğrulaması DEV-00 kapsamındadır. Bu görevler uygulama kodlama izni değildir.
