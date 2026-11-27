# PHASE-12 — Optional Conflict-safe Multi-device Sync
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
Opt-in encrypted full snapshot sync with CAS and explicit conflict review; no silent overwrite or automatic merge.
## Önkoşullar
PHASE-11 Accepted; explicit sync authorization.
## Bağlam (repo root altında docs/)
- [ architecture/SYNC.md ](../../architecture/SYNC.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ architecture/DATABASE.md ](../../architecture/DATABASE.md)
- [ decisions/ADR-0016-security-cloud-sync.md ](../../decisions/ADR-0016-security-cloud-sync.md)
- [ design/SCREEN_DETAILS.md ](../../design/SCREEN_DETAILS.md)
- UX: UX-25 sync/conflict, UX-24 restore/pause
- Quality: Q-CLOUD-01/02, Q-SEC-03/04, Q-FIN-02..04 restoration invariants, Q-REL-01
## Kapsam ve modüller
sync metadata row/local revision and provider adapter, owner-scoped remote head CAS/RLS, encrypted immutable snapshots, UI conflict
## Kapsam dışı
Realtime/CRDT/row merge/event store, background polling, service role client, automatic paid upgrade, plaintext/keys remote.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P12-T01 — REVISION
Bağımlılık: faz giriş kapısı.
Local datasetId/deviceId/revision and lastSyncedLocalRevision/baseRemoteVersion, syncable mutation increment atomic, device-specific state excluded. Snapshot encryption/AAD dataset+intended revision/version, bounded KDF cache unlocked only; no raw/keys.

**Kabul/kanıt:** Unit and DB mutation races, local restore pauses sync.

### P12-T02 — CAS
Bağımlılık: P12-T01. 
Private immutable blob upload then atomic owner head CAS expected opaque token + operation ID; verify path ownership, AEAD/hash/version, idempotent retry and orphan cleanup current+previous retention. Remote older/replay flagged, local dirty preserved on failure.

**Kabul/kanıt:** RLS/CAS simultaneous upload test, interruption, quota, orphan no current deletion.

### P12-T03 — CONFLICT
Bağımlılık: P12-T02. 
Clean local remote advanced -> staged encrypted restore only if unchanged; dirty local same remote -> CAS upload; both changed block; two encrypted copies preserved before explicit keep-local/use-remote, latest recheck and no auto merge. Password change new dataset explicit backup/recovery; disconnect/delete explicit.

**Kabul/kanıt:** Two device competing edits, local change during review, failure safe, no silent LWW.

### P12-T04 — UI
Bağımlılık: P12-T03. 
First explicit sync only; opt-in foreground coalescing if verified; status/revision, last sync, conflict summary decrypted locally, choices no default, backup evidence before discard, offline/quota errors; account deletion and restore/rebase.

**Kabul/kanıt:** Two test devices or separately isolated sessions; real cross-platform test before cross-platform claim.

### P12-T05 — FINAL
Bağımlılık: P12-T04. 
Run full cloud+local regression, portability, budget/cost and auth/retention verification. Update scope completion per platform and known risks; user acceptance and stop.

**Kabul/kanıt:** No future unattended task or external deploy without consent.

## Faz çıkış kapısı
Q-CLOUD-01/02 all pass, conflict versions preserved, real two-device/platform evidence where claimed; no P0/P1, no unapproved paid or deployment.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Opsiyonel CAS sync verified; scope only claims supported targets.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
