# PHASE-03 — Accounts, Transactions & Manual Entry
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
First end-to-end usable offline finance vertical slice: accounts, income/expense/transfer, categories/tags, templates and real overview.
## Önkoşullar
PHASE-02 Accepted.
## Bağlam (repo root altında docs/)
- [ product/SCOPE.md ](../../product/SCOPE.md)
- [ product/USER_FLOWS.md ](../../product/USER_FLOWS.md)
- [ design/SCREENS.md ](../../design/SCREENS.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ architecture/MONEY_CURRENCY.md ](../../architecture/MONEY_CURRENCY.md)
- [ architecture/FINANCIAL_ENGINE.md ](../../architecture/FINANCIAL_ENGINE.md)
- UX: UX-01,03..09,21 (accounts/transactions/rates), UX-02 privacy
- Quality: Q-FIN-01..05 UI/DB cross-check, Q-UX-01/02/04/05 (implemented screens), Q-REL-01
## Kapsam ve modüller
mobile features accounts, transactions, categories, templates, dashboard, settings; shared UI money/list/form; existing core/DB use cases
## Kapsam dışı
Payment/forecast fake values, auto capture, widgets, cloud; custom keypad or dashboard configuration.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P03-T01 — ACCOUNTS
Bağımlılık: faz giriş kapısı.
List/detail/edit/create cash/bank/card, opening equity and optional statement days, currency immutable once posted, archive history. Confirm no account create CTA. Show debt and assets separately, net worth vs operating cash; manual currency and historical FX support.

**Kabul/kanıt:** Account create/reopen offline, opening not income, archive no delete.

### P03-T02 — ENTRY
Bağımlılık: P03-T01. 
Shared amount-first editor income/expense/transfer, category for income/expense, account(s), local date, note/tag, manual FX two actual amounts. Last compatible account, system keyboard, validation, save once/idempotency, error preserves inputs. Template preview and confirmation.

**Kabul/kanıt:** Maestro/RNTL actual ledger effects, invalid decimals, offline, double tap, FX missing.

### P03-T03 — LIST
Bağımlılık: P03-T02. 
Date-grouped transactions, search/filter period/account/category/type/tags, no results vs empty, detail source/related history; edit append reversal/replacement, cancel confirmation, true refund, category/tag/template management archive. No raw content.

**Kabul/kanıt:** Signed direction, stable list, historic relations, duplicate no mutation.

### P03-T04 — OVERVIEW
Bağımlılık: P03-T03. 
Actual operating balance and month actual income/expense, recent 5 transactions; plans and safe-to-spend surface gated until 04/05 (not 0/fake). Reporting currency/manual rate editor; validated free rate provider adapter if available, rate provenance/date, stale/unknown, no network dependency.

**Kabul/kanıt:** Read model exact; change currency preserves original; privacy masks numbers/charts/accessibility.

### P03-T05 — VERIFY
Bağımlılık: P03-T04. 
Run critical happy and negative flows end-to-end on Android development build offline and restart, check TR/EN/theme/keyboard/200% font; iOS build/simulator if available separately. Record first checkpoint and test evidence.

**Kabul/kanıt:** Manual app usable with synthetic data, no real financial data until portable backup gate.

## Faz çıkış kapısı
Core manual paths, account/card/transfer/refund correct, actual UI tests and Android smoke; no placeholder pretending unimplemented features.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
İlk çalışan offline manuel finans uygulaması (sentetik veri).
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
