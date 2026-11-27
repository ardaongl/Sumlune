# PHASE-07 — Android Smart Capture — Bank Push
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Akbank and Ziraat notification-first capture, review-first and trusted explicit expense auto. SMS separate.
## Önkoşullar
PHASE-06 Accepted; Android listener/queue validation from 00 resolved.
## Bağlam (repo root altında docs/)
- [ architecture/SMART_CAPTURE.md ](../../architecture/SMART_CAPTURE.md)
- [ architecture/PLATFORM_BRIDGE.md ](../../architecture/PLATFORM_BRIDGE.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ architecture/PAYMENT_RECURRENCE.md ](../../architecture/PAYMENT_RECURRENCE.md)
- [ decisions/ADR-0014-smart-capture.md ](../../decisions/ADR-0014-smart-capture.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- UX: UX-19,20, UX-03 inbox, UX-21 settings
- Quality: Q-CAP-01..05 push subcases; Q-FIN-03/04 capture atomic and reversal; Q-UX-05; SMS subcases 10
## Kapsam ve modüller
Android Kotlin native module/listener/parser/queue; platform capture port; mobile smart_capture; three tables/account mapping migration
## Kapsam dışı
SMS receiver/permission, raw history, remote regex/LLM, background ledger writes, other bank claims.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P07-T01 — FIXTURE
Bağımlılık: faz giriş kapısı.
Verify official package allowlist and actual device notification formats for Akbank/Ziraat; user supplies fully redacted examples outside Git, create synthetic format fixtures. Never ask for OTP/full account/card/identity. No support claim without per-bank fixture + device proof. Unknown bank disabled.

**Kabul/kanıt:** If formats unavailable, mark bank blocked; framework tests synthetic not bank support.

### P07-T02 — NATIVE
Bağımlılık: P07-T01. 
NotificationListenerService opt-in source/bank toggles, native memory allowlist/positive settled parser, reject OTP/PIN/declined/unknown, sanitized structured envelope v1 only, canonical amount, distinct source key and strong reference HMAC; no raw persist/log/network. AES-GCM queue separate key, 7d/500 max drop new+count, ack only after commit; foreground drain/resume, no plaintext or headless required.

**Kabul/kanıt:** Device crash/retry/permission revoke/reboot/force-stop/overflow; queue and HMAC key lifecycle.

### P07-T03 — DEDUP
Bağımlılık: P07-T02. 
Candidates/mappings/rules and account hint HMAC migration, unique source retry vs conflicting notification update, strong ref scoped and validated; weak ±5 min (inferred ±24h review only) with merchant/account/currency/type/amount; no automatic weak merge. Distinct identical purchases preserved, link existing no journal.

**Kabul/kanıt:** Cross manual/push fixtures; retention and purge no replay.

### P07-T04 — RULES
Bağımlılık: P07-T03. 
All pending default, confirmed account/category, exact supported settled push expense, explicit merchant/version/max/currency rule; overlap/unknown/refund/transfer/card payment review. Atomically candidate/journal/postings/optional unique verified payment allocation; undo reversal, disable and no re-auto.

**Kabul/kanıt:** Failure remains pending; permission and rule checked again before write.

### P07-T05 — UI
Bağımlılık: P07-T04. 
Android inbox review/edit/approve/link/reject/separate/undo, setup bank status and OS permission, explicit opt-in, queue loss and unsupported UI; iOS manual/template only. Device restore/rotation disables auto and remaps; no sensitive logs.

**Kabul/kanıt:** Actual Akbank and Ziraat proof per bank, no test financial data leaked.

## Faz çıkış kapısı
Q-CAP push mandatory pass for each claimed bank. Missing bank evidence blocks bank-specific acceptance; user can explicitly approve a separately documented narrower Android checkpoint without marking full phase accepted, or resolve blocker. SMS not in manifest.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Doğrulanmış Android banka push capture; destek matrisi kanıtlı.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
