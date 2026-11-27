# Quality Matrix — PLAN-09A / Proposed

ID'ler blueprint task/acceptance evidence bağlantısı için stabil. Bu matris minimum mandatory behavior; ilgili ADR tüm edge case'leri ve UX-01..25 gereksinimlerini korur. Durumlar uygulama sonrası PROGRESS'e kaydedilir; şu an tüm testler Not run. P0 veri kaybı/yanlış ledger/secret leak/auth bypass; P1 kritik işlev bozuk, P2 noncritical UX/performance. Gated SMS/cloud/iOS feature kendi release gate'ine tabi; mock/policy-blocked başarı değildir.

| ID | Risk | Senaryo / kabul | Kanıt katmanı |
|---|---|---|---|
| Q-FIN-01 | P0 | Minor units TRY/JPY/KWD, parse, rounding, safe bounds, SQLite/JSON round-trip; no binary float | unit+native integration |
| Q-FIN-02 | P0 | Income/expense/transfer/opening/card liability, balanced postings, card payment gider değil | unit+DB |
| Q-FIN-03 | P0 | Atomic failure, rollback, FK, retry idempotency and mismatched payload | DB |
| Q-FIN-04 | P0 | Reversal/replacement/refund/date and allocation; no double count | unit+DB |
| Q-FIN-05 | P0 | FX clearing, actual amount/immutable snapshot, missing rate incomplete, reporting currency | unit+DB |
| Q-PAY-01 | P1 | Recurrence Jan31/leap/DST, 90d, missed due, idempotent generation | unit+DB |
| Q-PAY-02 | P0 | Partial/overdue, unknown amount, over-allocation reject, link existing/reversal reopen | unit+DB+UI |
| Q-PAY-03 | P0 | 100/3 rounding, card purchase full expense/statement remainder/principal once | unit+DB |
| Q-PAY-04 | P0 | Borrow/lend principal and interest, opening debt and payment | unit+DB |
| Q-PAY-05 | P1 | Local notification permission, reschedule, no due journal | native+UI |
| Q-INT-01 | P0 | Budget historical version, refund, category/overall overlap, actual vs plan | unit+DB |
| Q-INT-02 | P0 | Savings transfer no expense, reserve no double count | unit+DB |
| Q-INT-03 | P0 | Safe-to-spend excludes future income/limit, overdue/residual debt once, incomplete | unit |
| Q-INT-04 | P1 | Forecast 30/60/90 same series, negative day, unknown/FX, actual cash no replay | unit+UI |
| Q-INT-05 | P1 | Heatmap/period comparison zero/negative prior, annual subscription normalize vs actual | unit+UI |
| Q-CAP-01 | P0 | Akbank/Ziraat confirmed fixture, unsupported/OTP/declined no raw store, amount locale | Kotlin+device |
| Q-CAP-02 | P0 | exact replay/weak duplicate/real identical purchases, SMS+push+manual review | unit+DB |
| Q-CAP-03 | P0 | rule opt-in limit, unique match, parser version, SMS review-only, undo | unit+DB+UI |
| Q-CAP-04 | P0 | encrypted queue ack/crash/TTL/overflow/key unavailable, no plaintext | native+device |
| Q-CAP-05 | P1 | permission revoke, reboot/force-stop/OEM status and fallback; SMS distribution gate | device/policy |
| Q-WID-01 | P0 | masked payload no financial fields, generation race, lock/global hide | unit+native |
| Q-WID-02 | P1 | all six kinds compact/expanded, stale/midnight/corrupt/missing, refresh caveat | native+device |
| Q-WID-03 | P0 | quick add/deep link validates route+auth, no direct write/DB/key | UI+device |
| Q-SEC-01 | P0 | encrypted SQLCipher DB/WAL, lost key recovery no overwrite, backup exclusion | native+device |
| Q-SEC-02 | P0 | lock/enrollment change, cancel, app switcher, deep link, no sensitive flash | UI+device |
| Q-SEC-03 | P0 | backup known-answer AEAD/KDF, tamper/wrong password/limits, no raw/key | unit+native |
| Q-SEC-04 | P0 | Android/iOS portable restore, staging rollback/crash, migration and ledger validation | native+device |
| Q-SEC-05 | P0 | plaintext export explicit consent, CSV injection, temporary cleanup | unit+UI+device |
| Q-CLOUD-01 | P0 | encrypted only, RLS cross-user, no privileged client key, quota/local fallback | cloud integration |
| Q-CLOUD-02 | P0 | CAS race/retry, both versions preserved, explicit conflict, restore/pause/delete | cloud integration+UI |
| Q-UX-01 | P1 | onboarding/skip/account/no login/offline, add expense/income/transfer/template | RNTL+Maestro |
| Q-UX-02 | P1 | list search/filter/detail, form validation, keyboard, dirty back, commit success only | RNTL+Maestro |
| Q-UX-03 | P1 | planning create/settle, budget/goal/forecast drilldown, shared read model | RNTL+Maestro |
| Q-UX-04 | P1 | TR/EN, light/dark/system, small/standard, 200% font, contrast, screen reader, reduce motion | UI+manual |
| Q-UX-05 | P0 | privacy amounts/derived charts/accessibility, lock gate, permission denied, incomplete no false zero | UI+device |
| Q-PERF-01 | P2 | 10k journals benchmark save/list/overview/forecast/cold start; targets TEST_STRATEGY | release build benchmark |
| Q-REL-01 | P0 | fresh install, encrypted migration from previous supported schema, no destructive reset | device+DB |
| Q-REL-02 | P1 | reproducible local Android APK / iOS build, clean restart/offline, no secrets, dependency audit triage | build+device |

## Evidence and mapping
Each blueprint references its relevant Q IDs and UX IDs. Mandatory scenario evidence includes expected vs observed, command or manual steps, platform/SDK, result pass/fail/blocked/not-run, commit and sanitized artifact. All in-scope P0/P1 must pass, P2 targets measured and reviewed; no blanket coverage substitute. Test plan separate from test implementation. No tests run during planning.
