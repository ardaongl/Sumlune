# PHASE-11 — Optional Encrypted Cloud Backup
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Manual opt-in in-app encrypted backup upload/download without mandatory account or backend for local use.
## Önkoşullar
PHASE-06 and 09 local release accepted for relevant platform; explicit cloud phase and any external account/cost authorization.
## Bağlam (repo root altında docs/)
- [ architecture/SYNC.md ](../../architecture/SYNC.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ decisions/ADR-0016-security-cloud-sync.md ](../../decisions/ADR-0016-security-cloud-sync.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- UX: UX-25 auth/backup only, UX-24 integration
- Quality: Q-CLOUD-01, Q-SEC-03/04 regression, Q-UX-05; Q-CLOUD-02 sync later
## Kapsam ve modüller
mobile backup/sync feature, cloud provider adapter, Supabase candidate minimal auth/storage/RLS migrations, isolated test config
## Kapsam dışı
Realtime sync, row merge, production deployment or paid plan without permission, server plaintext/key, mandatory login.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P11-T01 — PROVIDER
Bağımlılık: faz giriş kapısı.
Verify current free tier, auth/email, quota/storage file limit and RLS owner policy; choose Supabase only after approved technical gate. Local emulator/test project with authorized account, no service_role client. If provider/cost incompatible, blocked/manual backup remains.

**Kabul/kanıt:** Document pricing date, quotas, actual tests; no automatic paid upgrade.

### P11-T02 — AUTH
Bağımlılık: P11-T01. 
Opt-in account for cloud only, login/logout/token storage via secure storage, no local lock bypass, account deletion/disconnect explicit and local data retained. TLS, auth expiry/rate limit/recovery UX.

**Kabul/kanıt:** No mandatory sign-in; offline local remains.

### P11-T03 — BACKUP
Bağımlılık: P11-T02. 
Reuse validated encrypted envelope, manual upload/list/download/delete owner scoped private immutable object; 20MiB and quota, minimal metadata, ciphertext only, user passphrase not provider. Restore via existing preview/replace, no silent overwrite, remote deletion explicit.

**Kabul/kanıt:** RLS cross-user denied, interrupted upload/retry, corrupted blob, no plaintext network/logs.

### P11-T04 — UI
Bağımlılık: P11-T03. 
Cloud backup status, last backup, manual actions, password lost warning, quota/error/blocked; no sync button yet. Preserve local backups and export; disconnect/token cleanup and remote deletion separate.

**Kabul/kanıt:** Q-CLOUD-01 tests, safe encrypted local restore, cost gate.

## Faz çıkış kapısı
RLS isolation, encryption at source, restore validation, auth/quota/offline and delete tests pass; only approved provider and no paid plan.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Opsiyonel uygulama içi şifreli cloud backup.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
