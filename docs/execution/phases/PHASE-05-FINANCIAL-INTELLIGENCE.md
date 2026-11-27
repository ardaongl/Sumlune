# PHASE-05 — Financial Intelligence & Analytics
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
All deterministic financial insights and complete Overview, no AI or backend.
## Önkoşullar
PHASE-04 Accepted.
## Bağlam (repo root altında docs/)
- [ architecture/FINANCIAL_INTELLIGENCE.md ](../../architecture/FINANCIAL_INTELLIGENCE.md)
- [ architecture/PAYMENT_RECURRENCE.md ](../../architecture/PAYMENT_RECURRENCE.md)
- [ architecture/MONEY_CURRENCY.md ](../../architecture/MONEY_CURRENCY.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- [ decisions/ADR-0013-financial-intelligence.md ](../../decisions/ADR-0013-financial-intelligence.md)
- UX: UX-15..18, UX-03 final, UX-11 annual subscription cost
- Quality: Q-INT-01..05, Q-UX-03 analytics, Q-UX-04/05, Q-REL-01 analytics migration
## Kapsam ve modüller
core budgeting/savings/forecasting/analytics; mobile budgets,savings,analytics,forecasting,dashboard; budgets/savings_goals and flags migration
## Kapsam dışı
LLM, ML spending prediction, arbitrary extrapolation, custom dashboard, analytics DB/cache table.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P05-T01 — MEASURES
Bağımlılık: faz giriş kapısı.
One shared exact metric contract: expense signed posting, income sign reversed, refund own date, reversal original valuation, local date and as-of, exclude principal/transfer/FX clearing; incomplete missing FX, no zero fabrication. Weekly Mon, month/year, comparable elapsed days, no % prior <=0.

**Kabul/kanıt:** Cross-check ledger fixtures across all read models.

### P05-T02 — BUDGET
Bağımlılık: P05-T01. 
Versioned effective_month overall/category budget, no rollover, %80/%100 thresholds, past unchanged, negative net visible, overlap not summed. budgets migration, UI list/editor/limit/progress/overrun.

**Kabul/kanıt:** Q-INT-01 positive/refund/FX/history.

### P05-T03 — SAVINGS
Bağımlılık: P05-T02. 
savings_goals linked one active asset account, operating flag, real/simulated reserve transfer distinguished, progress exact, no double count/no auto release; atomic use cases.

**Kabul/kanıt:** Q-INT-02 and actual transfer no expense.

### P05-T04 — PROJECTION
Bağımlılık: P05-T03. 
Shared operating cash classifier + obligation projection; 30/60/90 today..N−1, overdue once, liabilities residual and installment plan coverage all horizons, unknown/FX incomplete, future income excluded safe-to-spend. Forecast daily closing known plans including explicit future income toggle, no replay current actual, risk for undated debt, negative first day; no 30/60 independent rounding.

**Kabul/kanıt:** Q-INT-03/04 seeded fixtures and high coverage.

### P05-T05 — INSIGHTS
Bağımlılık: P05-T04. 
Week/month/year chart summary/drilldown, heatmap accessible labels, negative refunds separate, annual subscription run-rate weekly52/monthly12/yearly1 vs finite expected 12mo; actual vs planned label. Overview safe-to-spend and real charts; no masked derived leakage.

**Kabul/kanıt:** UI/RNTL/Maestro, locale/theme and incomplete states.

## Faz çıkış kapısı
Q-INT all and UI relevant subsets, coverage per module, 90-day deterministic exact calculation. No unverified totals.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Tam yerel finansal analiz, bütçe ve tahmin.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
