# PHASE-08 — Six Native Home-screen Widgets
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Six widgets use same snapshot and financial read models with strict privacy and safe deep links.
## Önkoşullar
PHASE-06 Accepted, PHASE-07 Accepted or explicitly isolated blocked capture with no widget dependency; renderer gate 00 resolved for target platform.
## Bağlam (repo root altında docs/)
- [ architecture/WIDGETS.md ](../../architecture/WIDGETS.md)
- [ architecture/FINANCIAL_INTELLIGENCE.md ](../../architecture/FINANCIAL_INTELLIGENCE.md)
- [ architecture/PLATFORM_BRIDGE.md ](../../architecture/PLATFORM_BRIDGE.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ decisions/ADR-0015-native-widgets.md ](../../decisions/ADR-0015-native-widgets.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- UX: UX-22 and home-screen widget surfaces; UX-07 quick add
- Quality: Q-WID-01..03, Q-SEC-02 widget interaction, Q-UX-05
## Kapsam ve modüller
mobile widget snapshot service/settings; platform publisher/renderers Glance/WidgetKit or validated Expo Widgets; no DB in extension
## Kapsam dışı
Lock screen, watch, Live Activities, direct ledger mutation, widget network/polling, duplicate renderer.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P08-T01 — SNAPSHOT
Bağımlılık: faz giriş kapısı.
Atomic envelope v1, per-kind discriminated masked/visible schema, max64KiB, only minimal formatted values; masked excludes numbers/count/labels, version/generation, expiry and privacy. Shared read models, no raw keys/DB. Serial publisher, 250ms normal debounce, privacy immediate, stale revision guards, restore/lock mask; widget cache OS caveat.

**Kabul/kanıt:** Unit tests masked payload leakage/race/expiry/invalid schema; no financial computation native.

### P08-T02 — FIRST
Bağımlılık: P08-T01. 
Daily expense/count and quick add safe route first; compact/expanded layout, native font/theme, explicit confirmation form; native capability selected in 00, same platform one renderer. iOS App Group and Android private storage, no backup.

**Kabul/kanıt:** Device deep link locked/unlocked and renderer smoke.

### P08-T03 — REST
Bağımlılık: P08-T02. 
Upcoming max3, monthly subscription normalized/next, budget selected scope, balance operating/default or selected, daily/quick add complete six. Small/medium responsive, incomplete/empty/stale placeholder, no wrong day at midnight/month end.

**Kabul/kanıt:** Each widget kind both sizes, two themes, unknown FX, no false zero.

### P08-T04 — SETTINGS
Bağımlılık: P08-T03. 
Kind scope and visibility consent, lock active cannot visible, global hide override, labels sanitization, app setup guidance. Ledger/payment/budget/FX/locale/restore triggers coalesced, app resume retry; publish failure does not rollback financial write.

**Kabul/kanıt:** Android launcher real refresh and mask, iOS own build/device status, no cache removal guarantee.

### P08-T05 — VERIFY
Bağımlılık: P08-T04. 
Run all Q-WID per target; deep link allowlist opaque UUID/auth, injection/stale route, explicit save, no direct write. Prebuild/rebuild widget preservation.

**Kabul/kanıt:** Record six kinds actual target platform; iOS proof not Android equivalent.

## Faz çıkış kapısı
All six Android widgets verified with privacy/deep link/refresh caveats; iOS target independent and blocked if device/signing unavailable. No financial privacy failure.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Altı native widget Android'de kanıtlı; iOS durum ayrı.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
