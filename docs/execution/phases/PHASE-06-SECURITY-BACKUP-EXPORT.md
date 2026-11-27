# PHASE-06 — Security, Portable Backup & Export
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Before real data use, verify durable encrypted backup and crash-safe restore; CSV/JSON explicit export.
## Önkoşullar
PHASE-05 Accepted; PHASE-00 crypto and PHASE-01 key/auth passed.
## Bağlam (repo root altında docs/)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ architecture/SYNC.md ](../../architecture/SYNC.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ architecture/SMART_CAPTURE.md ](../../architecture/SMART_CAPTURE.md)
- [ architecture/WIDGETS.md ](../../architecture/WIDGETS.md)
- [ decisions/ADR-0016-security-cloud-sync.md ](../../decisions/ADR-0016-security-cloud-sync.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- UX: UX-02,23,24
- Quality: Q-SEC-01..05, Q-UX-05, Q-REL-01
## Kapsam ve modüller
mobile backup/security/settings infrastructure; platform crypto/file/secure store; logical schema export and restore staging
## Kapsam dışı
Cloud auth/upload/sync, general CSV/JSON import, automatic destructive merge; no custom cryptography.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P06-T01 — KEYAUDIT
Bağımlılık: faz giriş kapısı.
Audit DB/WAL/temp/log/OS backup exclusion, separate keys, missing key recovery, biometric enrollment cancel, app background and deep link gate; no sensitive cache while locked. Test actual Android, iOS separately.

**Kabul/kanıt:** Q-SEC-01/02 pass or target platform blocked.

### P06-T02 — ENVELOPE
Bağımlılık: P06-T01. 
Versioned allowlisted logical snapshot consistent read transaction; canonical minor string, datasetId, schemaVersion, all financial/plan/budget/goal/rate relations. .sumlune-backup v1 AES-GCM/validated KDF, random salt/nonce, AAD, tag, bounded 20MiB/parameters, passphrase UTF8 NFC, no device/raw/queue/rules/secret. Known-answer/tamper test and cross-platform fixture.

**Kabul/kanıt:** No plaintext file, no password/key logs; wrong password safe.

### P06-T03 — RESTORE
Bağımlılık: P06-T02. 
Bounded parse/decrypt/schema/FK/ledger/alloc validation, preview counts/date, explicit replace fresh auth, staged encrypted DB new key, migrations/integrity checks, crash-safe swap + rollback state; current DB untouched on failure. Rebuild notifications/cache, widget masked and capture review-first/sync pause when implemented.

**Kabul/kanıt:** Crash before/after each swap state, old/new valid only; no automatic merge.

### P06-T04 — EXPORT
Bağımlılık: P06-T03. 
CSV/JSON explicit plaintext warning, fresh auth as required, readable major decimal/currency/date, versioned integer-string JSON, formula injection escape, temp no backup cleanup and file picker/share; last backup success real, user password loss warning.

**Kabul/kanıt:** Roundtrip encrypted Android↔iOS where device available; export no secrets.

### P06-T05 — REALDATA
Bağımlılık: P06-T04. 
Run restore from previous supported schema, corruption/wrong password/oversize/invalid financial invariants; test physical device auth and backups. Record target platform gates separately. Real user data permission only after Android local backup+restore verified; no Git uploads.

**Kabul/kanıt:** No user data fixtures; iOS portability proof pending if missing device, do not claim cross-platform verified.

## Faz çıkış kapısı
Android security/backup/restore/export mandatory pass; common format known-answer and portability checks on available iOS lane, iOS blocked if required device unavailable. No real data until safe Android recovery verified.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Güvenli kişisel kullanım adayı, yerel yedek/restore/export.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
