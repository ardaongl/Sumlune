# Backlog — planlama

| ID | Görev | Bağımlılık | Durum |
|---|---|---|---|
| PLAN-00 | Repo erişimi ve doküman baseline commit | GitHub yazma | Done |
| PLAN-01 | Mimari önerileri gözden geçir/onayla | Baseline | Done |
| PLAN-02 | Finansal invariants, money representation, hesap modeli | PLAN-01 | In progress: kayıt modeli Accepted, para/kur modeli sırada |
| PLAN-03 | ERD, kolon, constraint, index, migration | PLAN-02 | Pending |
| PLAN-04 | Recurrence, kart, taksit, debt, forecast politikaları | PLAN-02 | Pending |
| PLAN-05 | Capture parser, bankalar, dedup, queue, otomasyon | PLAN-02 | Pending |
| PLAN-06 | Widget snapshot/deep link sözleşmesi | PLAN-02 | Pending |
| PLAN-07 | Security, backup, cloud sync | PLAN-03/05/06 | Pending |
| PLAN-08 | Ekran ve kabul kriterleri | PLAN-02/04 | Pending |
| PLAN-09 | Test planı, görev bağımlılıkları, Codex handoff | PLAN-01..08 | Pending |
| DEV-00 | SDK uyumu ve native/SQLCipher spike | Açık kodlama onayı | Not authorized |
| DEV-01 | Dört reset implementation | DEV-00 + plan | Not authorized |

PLAN-01 onaylandı; PLAN-02 kayıt modeli kararı tamamlandı, Money & Currency Model sıradaki aktif karar. Koşullu stack doğrulaması DEV-00 kapsamındadır. Bu görevler uygulama kodlama izni değildir.
