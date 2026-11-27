# PHASE-04 — Payment & Recurrence
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Shared Payment Engine and calendar with actual-vs-plan separation, installments/debts, reminders.
## Önkoşullar
PHASE-03 Accepted.
## Bağlam (repo root altında docs/)
- [ architecture/PAYMENT_RECURRENCE.md ](../../architecture/PAYMENT_RECURRENCE.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ architecture/FINANCIAL_ENGINE.md ](../../architecture/FINANCIAL_ENGINE.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- [ decisions/ADR-0012-payment-recurrence.md ](../../decisions/ADR-0012-payment-recurrence.md)
- UX: UX-10..14, UX-03 upcoming, UX-23 notifications
- Quality: Q-PAY-01..05, Q-FIN-04 allocation, Q-UX-03 planning, Q-REL-01 payment migration
## Kapsam ve modüller
sumlune-core recurrence/installments; mobile payments/subscriptions/installments/debts/calendar/notifications; three tables and account additions
## Kapsam dışı
Autopay/bank transfers, automatic statement import, interest guessing, separate subtype engines, analytics forecast.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P04-T01 — RECURRENCE
Bağımlılık: faz giriş kapısı.
Pure local calendar once/weekly/monthly/yearly interval, end/count, original anchor and month-end, leap/DST, today inclusive 90-day horizon and on-demand/long offline batch, unique schedule/due key. Pause/cancel future only, preserve partial/settled.

**Kabul/kanıt:** Jan31/Feb/Mar, leap, DST, duplicate/restart and long offline fixtures.

### P04-T02 — SCHEMA
Bağımlılık: P04-T01. 
Schedules/occurrences/allocations exact accepted columns, FK/unique, partial remaining, required flag from ADR-0013 later/now as needed, payment capacity based on actual journal account movement and currency, cross-FX snapshot. Unknown NULL !=0, overdue derived. Atomic create/link, reversal allocation inactive, reopen; over-allocation reject.

**Kabul/kanıt:** Real DB migration/rollback and race/idempotency.

### P04-T03 — TYPES
Bağımlılık: P04-T02. 
Subscription/bill/rent/recurring via shared editor; installments full expense + liability at purchase, floor remainder last (100/3); card statement total minus known installment leaves, no duplicate obligation; debt/receivable principal transfer and actual interest separate, opening equity. Unknown statement due explicit.

**Kabul/kanıt:** Q-PAY-03/04 tests including duplicate principal and early payment.

### P04-T04 — UX
Bağımlılık: P04-T03. 
Planning hub calendar and type lists/detail/edit, due status, actual amount/full/partial/link existing, cancel/skip guards, monthly dates, reminder controls and Overview upcoming 3. User sees amount vs cash obligation clearly.

**Kabul/kanıt:** Create/settle/reverse on Android, actual ledger only after confirm.

### P04-T05 — REMIND
Bağımlılık: P04-T04. 
Local Expo notification adapter, permission rationale, deterministic ID, OS capacity, reconcile on resume/change/settle, safe labels, no exact delivery promise. Permission denied retains calendar.

**Kabul/kanıt:** Device notification and cancellation, no due-time journal.

## Faz çıkış kapısı
Q-PAY mandatory all supported Android and core, payment allocation reversal Q-FIN-04, UI planning subset pass, coverage and migration.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Çalışan ödeme/taksit/borç takvimi ve yerel hatırlatmalar.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
