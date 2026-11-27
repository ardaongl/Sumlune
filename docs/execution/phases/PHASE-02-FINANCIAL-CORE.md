# PHASE-02 — Financial Core & Persistence
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Dengeli ledger ve exact money; SQLite tek gerçek kaynak; atomic use cases ve derived balance.
## Önkoşullar
PHASE-01 Accepted.
## Bağlam (repo root altında docs/)
- [ architecture/FINANCIAL_ENGINE.md ](../../architecture/FINANCIAL_ENGINE.md)
- [ architecture/MONEY_CURRENCY.md ](../../architecture/MONEY_CURRENCY.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ decisions/ADR-0006-double-entry.md ](../../decisions/ADR-0006-double-entry.md)
- [ decisions/ADR-0010-money-currency.md ](../../decisions/ADR-0010-money-currency.md)
- [ decisions/ADR-0011-database-architecture.md ](../../decisions/ADR-0011-database-architecture.md)
- UX: UX-04/05/07/08 domain contracts, UI PHASE-03
- Quality: Q-FIN-01..05 (allocation alt kısmı PHASE-04), Q-REL-01 (core migration)
## Kapsam ve modüller
sumlune-core money/currency/accounting/transactions; mobile infrastructure/database, accounts/transactions application ports; artımlı core migrations
## Kapsam dışı
Payment schedule, actual transaction screens, capture, budget, server, cache balance tables; gerçek veri reset.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P02-T01 — MONEY
Bağımlılık: faz giriş kapısı.
ISO exponent TRY/JPY/KWD, parse locale string without float, signed minor safe integer, BigInt intermediate/overflow, canonical integer-string wire, Decimal.js HALF_UP; deterministic clock/id/rate ports. Currency formatter contract. Test negative and boundary.

**Kabul/kanıt:** Exact conversion and rounding; no silent overflow.

### P02-T02 — LEDGER
Bağımlılık: P02-T01. 
Accounts asset/liability/income/expense/equity/system; posting debit+/credit−; each currency sum zero, at least two nonzero. Income/expense/transfer/card purchase/payment/opening/refund/reversal/replacement; FX clearing each currency, immutable snapshots, original FX card amount metadata. No credit limit cash, no double expense.

**Kabul/kanıt:** Fixtures 500 card+payment, opening liabilities, multi FX transfer, refund cap; 100+ seeded valid/invalid cases.

### P02-T03 — SCHEMA
Bağımlılık: P02-T02. 
Drizzle migration accounts/categories/journal_entries/postings/tags/transaction_tags/templates/exchange_rates/journal_rate_snapshots/settings as needed. UUID, FK RESTRICT, type/check safe bounds, partial unique category/system/reversal, index, idempotency key. Versioned migration and backup-safe failure. Real Expo SQLCipher adapter; actual SQL transaction contains aggregate validator.

**Kabul/kanıt:** Migration old fixture, foreign_key_check/integrity_check, transaction crash/rollback; no orphan entries.

### P02-T04 — USECASE
Bağımlılık: P02-T03. 
Repository ports + transaction application use cases, exact derived balances; same command key returns existing, differing payload rejects; append reversal/replacement same transaction, metadata update trace; refund relation/cap and original snapshot. Query history read model, manual rate cache and missing-rate incomplete; automatic provider only after free/accuracy verification, manual fallback remains.

**Kabul/kanıt:** No independent balance mutation; tests for idempotency conflicts and same-value distinct transactions.

### P02-T05 — GATE
Bağımlılık: P02-T04. 
Core module coverage, unit/property, integration actual DB and native bridge, inspect dependency boundary and migration. Record Q-FIN full vs partial subcases.

**Kabul/kanıt:** No actual payment allocation yet; carry Q-FIN-04 allocation subcase to 04.

## Faz çıkış kapısı
Exact money and core financial Q-FIN required subcases pass; coverage thresholds per implemented module, real SQLCipher migration/bridge evidence. No P0/P1.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Tested ledger API and persistence; UI next.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
