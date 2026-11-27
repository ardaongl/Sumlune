# PHASE-09 — Local Product Hardening & Release
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Release-ready local product, regression, benchmark, migration/recovery, reproducible installable Android package and separate iOS readiness.
## Önkoşullar
PHASE-01..08 accepted for target local release; isolated optional/native blockers require explicit scope-specific release decision, never claim missing feature.
## Bağlam (repo root altında docs/)
- [ engineering/TEST_STRATEGY.md ](../../engineering/TEST_STRATEGY.md)
- [ engineering/QUALITY_MATRIX.md ](../../engineering/QUALITY_MATRIX.md)
- [ engineering/DEFINITION_OF_DONE.md ](../../engineering/DEFINITION_OF_DONE.md)
- [ product/SCOPE.md ](../../product/SCOPE.md)
- [ product/ACCEPTANCE_CRITERIA.md ](../../product/ACCEPTANCE_CRITERIA.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- UX: UX-01..24 all relevant target, UX-25 later
- Quality: All non-cloud Q groups, push-only Q-CAP, Q-PERF-01, Q-REL-01/02; SMS separately 10
## Kapsam ve modüller
Existing packages/features, test/CI/release docs, scripts; no new feature scope
## Kapsam dışı
Store submission, paid build/signing subscription, SMS variant, cloud, new feature redesign; no claims for untested platform.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P09-T01 — TRACE
Bağımlılık: faz giriş kapısı.
Audit scope 35+4, 25 UX families, 38 Q groups via SCOPE_TRACEABILITY; distinguish full/push-only/SMS gated/iOS/cloud pending. Run regression all core and relevant UI/integration native E2E, coverage and failure cases. No mock-as-proof.

**Kabul/kanıt:** Every mandatory subcase and prior migration passed for target; unresolved P0/P1 block.

### P09-T02 — BENCH
Bağımlılık: P09-T01. 
Synthetic 10k journals/20k postings/20 accounts/100 plans; release device, p95 save/list/overview/90d, cold 5 and UX time-on-task. Record methodology exact, investigate index/query before caches; P2 deviations reviewed.

**Kabul/kanıt:** Performance target not silently relaxed; no P0/P1 waiver.

### P09-T03 — UXQA
Bağımlılık: P09-T02. 
TR/EN, light/dark/system, small/standard, 200% font, contrast, screen reader/reduce motion, back/keyboard, privacy/screenshot caveat, offline, denied permission, stale rates/empty.

**Kabul/kanıt:** Manual screenshots sanitized and evidence, no unfinished controls.

### P09-T04 — PACKAGE
Bağımlılık: P09-T03. 
Reproducible signed Android APK local, no real signing material in Git, actual install/restart/migration/restore smoke, manifest no SMS permission. iOS build/simulator, real-device/signing if available; record separate release gate. Audit dependencies/licenses and secrets. No publishing without explicit instruction.

**Kabul/kanıt:** Artifact location/hash outside Git if binary, exact build commands and device evidence.

### P09-T05 — HANDOFF
Bağımlılık: P09-T04. 
README run/build/install/backup/recovery instructions, supported bank/platform matrix, limitations, release notes, known risks. User acceptance after evidence, no auto next phase. Cloud/SMS remain planned.

**Kabul/kanıt:** Release decision per platform and enabled capability; don't label 100% all features.

## Faz çıkış kapısı
In-scope mandatory Q pass, no P0/P1, benchmark and P2 review, Android signed install and recovery. iOS store/release readiness separate; if unavailable remain blocked.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Android kişisel kullanım release adayı; SMS/cloud ayrı.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
