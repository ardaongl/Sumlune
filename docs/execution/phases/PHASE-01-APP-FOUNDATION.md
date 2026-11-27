# PHASE-01 — Application Foundation & Design System
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Çalışan güvenli uygulama iskeleti, ortak UI dili ve gerçek offline onboarding; finansal feature'lara hazır altyapı.
## Önkoşullar
PHASE-00 Accepted; core Android SDK/DB/crypto gate passed.
## Bağlam (repo root altında docs/)
- [ architecture/MODULES.md ](../../architecture/MODULES.md)
- [ architecture/DEPENDENCY_RULES.md ](../../architecture/DEPENDENCY_RULES.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ design/DESIGN_SYSTEM.md ](../../design/DESIGN_SYSTEM.md)
- [ design/DESIGN_TOKENS.md ](../../design/DESIGN_TOKENS.md)
- [ design/COMPONENTS.md ](../../design/COMPONENTS.md)
- [ design/SCREENS.md ](../../design/SCREENS.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- [ product/USER_FLOWS.md ](../../product/USER_FLOWS.md)
- UX: UX-01,02,03,21,23 (foundation alt kapsamı)
- Quality: Q-UX-01 (onboarding), Q-UX-04 (theme/i18n), Q-UX-05 (privacy/auth), Q-SEC-01/02 (local security), Q-REL-01 (initial DB)
## Kapsam ve modüller
apps/mobile app, src/core/providers/infrastructure/security; sumlune-ui tokens/primitives, sumlune-platform security/capability
## Kapsam dışı
Financial posting UI, plans, analytics, capture, widget renderer, cloud; sahte dashboard tutarı.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P01-T01 — ARCH
Bağımlılık: faz giriş kapısı.
Public package boundaries, feature-first folder yalnız ihtiyaçla, composition root ve repository/native port wiring. Query read cache, Zustand UI only. ESLint import boundary veya küçük architecture test; no core RN/network/DB import.

**Kabul/kanıt:** Lint/typecheck + forbidden import test.

### P01-T02 — UI
Bağımlılık: P01-T01. 
Pure Apple tokenları light/dark/system; iOS system, Inter Android license/fallback, semantic accessible accent variants; grouped row, button, money display/privacy, form sheet, status/empty/error/loading, dev-only playground. 48dp/52dp, 20dp, dynamic font, reduce motion; no hardcoded theme.

**Kabul/kanıt:** TR/EN, contrast pairs, 200% font, keyboard/safe area smoke; no paid design service.

### P01-T03 — ROOT
Bağımlılık: P01-T02. 
Expo Router root boot/migrate/recovery/onboarding/auth, 4 tabs + center Add sheet action, stable previous tab on dismiss. Onboarding 3 steps, skip/restore route gated until implemented, TRY default; no forced login or permissions. Settings locale/theme/privacy persistence; absent feature hide or clear unavailable.

**Kabul/kanıt:** RNTL root/route, back, skip, offline, dark and locale.

### P01-T04 — KEY
Bağımlılık: P01-T03. 
Production-shaped SQLCipher random device key, SecureStore separation UI auth, no existing DB overwrite on missing key. Migrations transaction, no backup of key/DB, app lifecycle cover and handle/cache cleanup. Opt-in biometric lock, device credential fallback supported, deep link gating, masked labels.

**Kabul/kanıt:** Q-SEC-01/02 device proof; failure no reset, no sensitive flash.

### P01-T05 — CI
Bağımlılık: P01-T04. 
Working pnpm fast verification, Linux CI only budget-safe, tests for theme/validation/lock, docs actual commands. Android build and iOS lane status.

**Kabul/kanıt:** No stub tests claiming full app; no real financial data until backup phase passes.

## Faz çıkış kapısı
Offline onboarding/root/auth/settings/theme functional; security gate Q-SEC-01/02 relevant Android device pass; UI state and import boundaries pass.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Açılan güvenli app, gerçek onboarding ve tema; kayıt motoru henüz yok.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
