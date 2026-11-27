# Testing & Quality Strategy — PLAN-09A / Proposed

ADR-0009 koşullu teknoloji yığını ve ADR-0006..0017 kabul edilmiş ürün/mimari sözleşmeleri. Bütçe ilkesi: risk temelli test piramidi, yerel/ücretsiz çalıştırma; kapsam/finansal güvenlik azaltılmaz. Bu doküman test planıdır, çalıştırılmış test yok.

## 1. Katman ve araçlar
| Katman | Araç (uyumluluk şartlı) | Zorunlu kanıt |
|---|---|---|
| Pure core | Vitest | deterministic unit + seeded invariant/property-style tests (basit generator; fast-check ancak gerekirse) |
| Persistence | gerçek SQLite integration + gerçek Expo/SQLCipher native smoke | FK/constraint, atomic write, rollback, migration, integer bridge, key/WAL |
| Capture | Kotlin JVM fixture tests + Android instrumented/manual device | positive/negative bank template, no raw, queue/permissions/dedup |
| UI/application | Jest + React Native Testing Library | kritik form, status, validation, auth, theme/i18n; davranış odaklı, snapshot yığını yok |
| Native | Kotlin/Swift platform tests gerektiğinde + device smoke | widget renderer/refresh/privacy, notification, lock/key, backup |
| E2E | Maestro aday (local) | seçili happy path + kritik failure; OS prompt/launcher/biometric gerçek cihaz manuel gate |
| Cloud (ayrı faz) | integration with isolated test project or local emulator + RLS/CAS tests | cross-user denial, encrypted only, conflict/retry; no prod keys |

Core ve DB testleri ayrı: masaüstü SQLite adapter SQL semantiğini kontrol eder, SQLCipher/Expo bridge kanıtı değildir. Mock UI success cihaz veya crypto testi değildir. Test araçları SDK ile DEV-00 doğrulanır; failure açık ADR, yeni bağımlılık gerekçeli. Gerçek banka verisi/secret/recovery parola/log repo yok; fixtures sentetik veya tamamen anonimleştirilmiş.

## 2. Risk temelli zorunlu senaryolar
Kabul kriterleri [ACCEPTANCE_CRITERIA](../product/ACCEPTANCE_CRITERIA.md), mimari ADR ve [QUALITY_MATRIX](QUALITY_MATRIX.md) ID'leri tek test traceability kaynağı. Her kritik invariant positive/negative/boundary + atomic failure test. Yeni bug'a önce regression test; nondeterministic clock, timezone, FX, UUID ve random seed inject. Test order bağımsız; no live FX/API varsayılan; fake provider. Property-style seed kaydedilir, 100+ valid/invalid cases per critical invariant hedefi, failure reproducible. No flaky retry to hide failure.

## 3. Coverage ve quality gates
- Pure core financial modules (money, ledger, recurrence, analytics) hedef >=95% line, >=90% branch; CI enforce ancak runner/coverage config doğrulandıktan sonra. Yeni feature kritik branch'leri eksik bırakamaz. Generated code, type-only declarations ve fixture excluded açıklanır; business logic exclude yok. Coverage tek başarı ölçütü değil. UI/native global coverage sayısı zorunlu değil; matrix critical behavior %100 passed. No arbitrary snapshot count. 
- Her görev: ilgili tests + typecheck/lint; her faz: full fast suite, format check, lint, typecheck, unit, integration ve kapsamındaki E2E/native build/manual evidence. Zorunlu gate skipped/failed/blocked -> faz Ready for review olamaz; unrelated unavailable platform açıkça not applicable/blocked (gerekçeli); sonraki faz geçişi kullanıcı onayı. Dev-only technical spike gate proof, ürün özelliği tamamlandı iddiası yok. 
- Release: sıfır açık P0 (veri kaybı, yanlış bakiye, auth bypass, raw/secret leak), P1 (kritik akış unusable/crash); bütün in-scope mandatory matrix pass, clean migration/backup restore, Android signed APK smoke, iOS build/simulator + gerçek cihaz kanıtı gerekiyorsa iOS release ayrı blocked. SMS policy/device gate geçmezse no SMS variant release; notification/manual sürümde açık capability. Cloud gate ayrı; local release blocker değil. Unsupported feature as complete yok. 
- Kanıt formatı: gate/task/test IDs, exact command, exit code, count pass/fail/skip, coverage report path, commit SHA, platform/OS/device/SDK (sensitive IDs yok), timestamp, screenshot/log sanitize, not-run reason. Self-approval yok. 
- Definition of Done [DEFINITION_OF_DONE](DEFINITION_OF_DONE.md), progress ve checkpoint PLAN-09B'de kesinleşecek.

## 4. Düşük maliyetli CI / cihaz matrisi
Yerel pnpm scripts contract: format:check, lint, typecheck, test:unit, test:integration, test:coverage, test:e2e, verify (fast gates). İsimler öneri, gerçek script yazılmadı; blueprint seçili SDK ve scriptleri doğrular. GitHub Actions Linux fast suite push/PR; lockfile/cache, no paid runners by default; macOS/iOS/Android native build yalnız ilgili faz/manual dispatch veya local, ücretsiz kota kontrolü. No secrets in logs, dependency lock/pinned SDK, audit high severity triage, no automatic paid build. Local Android emulator + en az bir gerçek Android cihaz (Akbank/Ziraat fixture/permission/widget), iOS simulator + gerçek iOS cihaz gerektiğinde; Mac/Xcode/signing koşulları DEV-00. API min/target, Android OS sürümleri, iOS deployment target seçilen SDK ile doğrulanır; gerçek cihaz availability bilinmiyor. Android modern + minimum supported emulator hedef; iOS minimum + current simulator mümkünse; 1 small/1 standard screen, 200% text, TR/EN/light/dark. No device farm zorunlu.

## 5. Performans hedefleri (öneri, benchmark sonrası doğrulanır)
Temsili seed: 10k journal/20k+ postings, 20 accounts, 100 plans; sentetik, release build, cihaz ve sample count kaydı. Warm transaction save p95 <=300ms (DB+validation, network hariç), common list query p95 <=200ms, overview/read-model p95 <=500ms, 90-day forecast <=500ms, cold usable screen <=3s hedef (auth/device/initial migration ayrı). 20 ölçüm minimum, warmup hariç; cold 5 tekrar ve median/max. UX common expense 3–5sn hedef, manuel time-on-task ayrı. Memory/scroll jank profile if needed; performans hedefi kaçarsa önce query/index/pagination, gereksiz cache/backend yok. Hedefler garanti değil; cihazla ölçülüp sapma/iyileştirme açık review. Security/financial invariants asla performance adına düşürülmez.

## 6. Açık doğrulamalar
SDK/package/SQLCipher/crypto/Glance/WidgetKit/Expo Widgets, SMS permission/installer/policy, banka formatı, iOS signing/device, FX provider, cloud quota/RLS. DEV-00 matrix ve faz-specific gates. Test stratejisi onayından sonra PLAN-09B ayrı goal prompts ve progress control; kodlama ayrı yetki. 
