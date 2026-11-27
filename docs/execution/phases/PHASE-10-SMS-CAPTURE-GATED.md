# PHASE-10 — Optional Gated Android SMS Capture
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Add Android review-only new bank SMS capture if permitted, without compromising notification-only build.
## Önkoşullar
PHASE-07 push infrastructure accepted; preferably PHASE-09 local checkpoint. Explicit SMS phase authorization and current policy/installer gate.
## Bağlam (repo root altında docs/)
- [ architecture/SMART_CAPTURE.md ](../../architecture/SMART_CAPTURE.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ decisions/ADR-0014-smart-capture.md ](../../decisions/ADR-0014-smart-capture.md)
- [ engineering/QUALITY_MATRIX.md ](../../engineering/QUALITY_MATRIX.md)
- UX: UX-19/20 SMS subset
- Quality: Q-CAP-01..05 SMS subcases, Q-SEC-01/02/05 regression, Q-REL-02 manifest
## Kapsam ve modüller
Android SMS-enabled build variant, Kotlin receiver/parser, capture inbox/source settings; reuse queue/ledger
## Kapsam dışı
READ_SMS/history scan, default SMS app, policy evasion via notification reading, OTP, SMS auto, iOS SMS.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P10-T01 — POLICY
Bağımlılık: faz giriş kapısı.
Recheck Android RECEIVE_SMS hard restricted installer allowlist and Play declaration/approval for money management, personal APK behavior on actual device; no policy circumvention. If not authorized, status Blocked, notification-only APK unchanged.

**Kabul/kanıt:** Current official links, device grant/deny evidence; approval where distribution requires.

### P10-T02 — VARIANT
Bağımlılık: P10-T01. 
Separate manifest/receiver config so notification-only build has no SMS permission. Explicit opt-in, sender allowlist (verify on device, no guessing), incoming SMS_RECEIVED only, native memory positive match; multipart and spoof risk review.

**Kabul/kanıt:** Inspect both manifests, denied/revoke fallback, no raw store.

### P10-T03 — PARSER
Bağımlılık: P10-T02. 
Akbank/Ziraat actual redacted templates and synthetic tests; same structured queue/HMAC/dedup, no raw data. SMS always review, push/SMS strong match link suggestion and weak review. Reject OTP/failed/pending.

**Kabul/kanıt:** No SMS auto rule, even matching merchant limit; identical purchases remain distinct.

### P10-T04 — VERIFY
Bağımlılık: P10-T03. 
Real-device policy+permission and parser evidence per bank, queue restart, manual approval atomic, no duplicate with push/manual, lock/restore regression, build separate APK only if valid.

**Kabul/kanıt:** Blocked if gate fails; no local release rollback or false supported claim.

## Faz çıkış kapısı
Policy/installer permission and each claimed bank SMS device test pass; review-only and no permission in base variant.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
İzinli SMS varyantı veya belgelenmiş blocked; local sürüm bağımsız.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
