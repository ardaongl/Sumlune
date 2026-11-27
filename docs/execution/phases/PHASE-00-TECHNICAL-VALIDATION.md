# PHASE-00 — Technical Validation & Bootstrap
**Durum:** Not started / ayrı yürütme izni gerekir. **Plan:** ADR-0019. 
## Goal
En küçük çalışır RN/Expo workspace ve Android development build ile pahalı mimari riskleri erkenden doğrula. iOS desteğini ayrı kanıtla; üretim finans verisi kullanma.
## Önkoşullar
Açık kullanıcı geliştirme izni; hiçbir önceki faz yok.
## Bağlam (repo root altında docs/)
- [ architecture/TECH_STACK.md ](../../architecture/TECH_STACK.md)
- [ architecture/MODULES.md ](../../architecture/MODULES.md)
- [ architecture/DEPENDENCY_RULES.md ](../../architecture/DEPENDENCY_RULES.md)
- [ architecture/SECURITY.md ](../../architecture/SECURITY.md)
- [ architecture/SMART_CAPTURE.md ](../../architecture/SMART_CAPTURE.md)
- [ architecture/WIDGETS.md ](../../architecture/WIDGETS.md)
- [ architecture/MONEY_CURRENCY.md ](../../architecture/MONEY_CURRENCY.md)
- [ decisions/ADR-0009-conditional-tech-stack.md ](../../decisions/ADR-0009-conditional-tech-stack.md)
- UX: UX-01/02 için yalnız teknik smoke, gerçek ekran değil
- Quality: Q-FIN-01 (bridge), Q-SEC-01 (key/DB), Q-SEC-03 (crypto spike), Q-CAP-04/05 (queue/lifecycle spike), Q-WID-01/02/03 (renderer spike), Q-REL-02 (dev build); partial evidence, full feature değil
## Kapsam ve modüller
apps/mobile, packages/sumlune-core, sumlune-ui, sumlune-platform; root workspace, scripts, CI skeleton, docs/execution/TECHNICAL_VALIDATION.md
## Kapsam dışı
Ürün ekranları, gerçek finans kayıtları, banka parser üretim desteği, cloud project, SMS izni dahil etme, ücretli EAS/CI, tüm paketleri peşinen kurma.
## Codex çalışma talimatı — bu dosya goal prompt'tur
Bu dosyayı kullanıcı açıkça çalıştırma talimatıyla verirse yalnız bu fazın kapsamı yetkilidir. Sadece dosyayı okumak, sonraki faza geçme izni değildir. Önce repo root, git status, branch/HEAD; kullanıcı değişikliklerini koru. AGENTS.md, README.md, docs/execution/CURRENT_STATE.md, DECISION_REGISTER.md, MASTER_PLAN.md, PROGRESS.md, SESSION_HANDOFF.md, CODEX_EXECUTION_PROTOCOL.md, docs/engineering/TEST_STRATEGY.md, QUALITY_MATRIX.md ve DEFINITION_OF_DONE.md oku. İlgili kaynakları aşağıdan aç; önceki sohbeti varsayma. Accepted ADR üstün; çelişki, eksik prerequisite veya koşullu stack başarısızlığı varsa Blocked kaydet, güvenli alternatif sun ve onay bekle. Başka faza taşan refactor/özellik yapma. Kullanıcı onayıyla active phase'i PROGRESS'e yaz; bir defada bir task. Task'ın ilgili testini önce/beraber yaz, uygulama, doğrula. Bir task tamamlanmadan diğerine geçme; limit yaklaşırsa çalışan checkpoint veya açık WIP/Blocked, handoff ve gerçek SHA. Mevcut kodu gereksiz değiştirme; no paid service, no secrets, no real finance fixture. 
## Doğrulama ve çıktı
Root'ta mevcut sözleşmeye göre `pnpm format:check`, `pnpm lint`, `pnpm typecheck`, `pnpm test:unit`, `pnpm test:integration`, `pnpm test:coverage`, `pnpm verify`; ilgili `pnpm test:e2e` ve native build/test komutları. PHASE-00'da script yoksa oluştur ve gerçek komutu kaydet; stub/exit 0 yasak. Native komutları doğrulanmış TECHNICAL_VALIDATION ve yerel ortamdan seç; sürüm/komut uydurma. Her Q için ilgili alt assertion ve target platform kaydı; tüm Q değilse Partial. Test/cihaz evidence'da exact command/manual steps, exit, passed/failed/skipped, expected/observed, SDK/OS, tested code SHA, sanitize artifact; eksik mandatory kontrol Blocked. Core coverage >=95% line/90% branch (mevcut modüller); P0/P1 çözülmeden Ready for review yok. P2 ölç ve review. 
Commit küçük, Conventional Commits; code checkpoint SHA'yı doğrula; ayrı docs-only evidence commit gerekebilir. PROGRESS task state/kanıt, evidence dosyası ve SESSION_HANDOFF güncelle; CURRENT_STATE sadece faz geçişinde. Scope change veya paid external action için açık izin. Push yalnız kullanıcı yetkisi/branch politikası ile; force/reset yok. Final rapor: goal, tamamlanan/blocked IDs, değişen dosya, tests/coverage/build/platform, kanıt SHA, risk, sonraki exact task. Ready for review ise dur ve kullanıcı kabulünü iste; sonraki faza kendiliğinden geçme.
## Sıralı görevler
### P00-T01 — ENV
Bağımlılık: faz giriş kapısı.
Yerel Node/pnpm/JDK/Android SDK/adb/Xcode ortamını kontrol et; mevcut Git durumunu koru. Expo SDK/RN/React/Node/pnpm/TS sürüm ve lisans matrisi oluştur, official docs ve lockfile ile gerekçelendir. Android min/target ve iOS deployment target SDK'ya göre kaydet. Kullanıcının cihazı yoksa cihaz kanıtı blocked; gerçek olmayan ortamı başarı gösterme.

**Kabul/kanıt:** Version matrix, exact commands, platform flags; no secrets.

### P00-T02 — WORKSPACE
Bağımlılık: P00-T01. 
Minimum pnpm workspace ve strict TS, Expo Router shell, üç paket public exports, app composition root; compatible dev build, prebuild/config plugin/autolinking. Native source preservation test. .gitignore env, signing keys, SQLite, backups. Root format/lint/typecheck/test:unit/test:integration/test:coverage/test:e2e/verify sözleşmesini yalnız gerçek çalışan scriptlerle başlat; henüz uygulanmayan gate açık not-run. No empty layers.

**Kabul/kanıt:** Fresh install frozen lockfile; import boundaries and minimal run.

### P00-T03 — DB
Bağımlılık: P00-T02. 
Disposable SQLCipher DB aç, wrong key fail, SQLite/WAL plaintext kontrol, SecureStore key round-trip/reinstall/missing key, Drizzle migration and rollback, FK; signed safe integer sınırı ve integer-string JSON/native roundtrip, exact aggregation. Test fixture ile sınırı aşan amount reddi.

**Kabul/kanıt:** Gerçek Expo native adapter kanıtı; desktop SQLite tek başına yeterli değil.

### P00-T04 — CRYPTO
Bağımlılık: P00-T03. 
Platform AES-256-GCM + PBKDF2-SHA256 v1 600k adayının bilinen cevap/Android-iOS format uyumu, tamper/wrong key, KDF latency, random nonce. Native APIs veya doğrulanmış compatible package; algoritma yazma.

**Kabul/kanıt:** Başarısız crypto güvenli blok; plaintext fallback yok.

### P00-T05 — NATIVE
Bağımlılık: P00-T04. 
Android NotificationListenerService permission, allowlist synthetic notification, structured encrypted queue prototipi, resume drain, process death/reboot/force-stop sonuçlarını kaydet. SMS permission manifest'te yok. Expo Widgets daily+quickAdd proof: small/medium, masked payload, deep link, prebuild, iOS App Group ve Android resize; destek yoksa tek platform fallback Glance/WidgetKit belgele.

**Kabul/kanıt:** Banka desteği iddia etme. Auth prompt, widget cache ve native permission sınırları kanıtlanır.

### P00-T06 — GATE
Bağımlılık: P00-T05. 
Doğrulanan stack/renderer/crypto seçimlerini TECHNICAL_VALIDATION ve gerekirse ADR-0009 ek kararı ile kaydet; değişiklik gerekiyorsa owner approval. Android working dev build ve iOS ayrı build/simulator status; cloud/FX provider canlı kurulum yok. CI fast suite mevcut kodda koşsun.

**Kabul/kanıt:** Temel Android DB/crypto/bootstrap engeli giderilmeden 01 yok; iOS unsupported status ayrı, sonraki iOS release gate zorunlu.

## Faz çıkış kapısı
Android minimum dev build + SQLCipher/secure key/crypto core spike + workspace checks geçti. Native capture/widget spike sonuçları kanıtlı veya ilgili capability blocked ve owner review; core'a etkisi yoksa kapsam daraltmadan ilerle. iOS lane kendi kanıtı olmadan verified değil.
Önceki fazların ilgili regression'ları da geçer. Platform lane ve capability status ayrı; kapsam azaltımı owner ADR olmadan yok.
## Beklenen çalışır checkpoint
Çalışan development shell ve teknik karar matrisi; release veya banka desteği değil.
## Oturum devri
PROGRESS ve SESSION_HANDOFF: tested SHA, evidence path, last verified task, next task ID, platform/capability blocker, run commands, scope deviations. Faz tamamlanınca Ready for review; yalnız kullanıcı Accepted yapar. Bir sonraki dosyayı kendin başlatma.
