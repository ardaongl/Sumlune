# Test stratejisi — Proposed

| Katman | Test |
|---|---|
| Pure core | Vitest unit + property-based: para, balanced postings, recurrence, bütçe, tahmin |
| Repository | Gerçek SQLite integration, transaction, unique constraint, migration |
| Parser | Sentetik/maskeli banka fixture, OTP, başarısız işlem, dedup, iade |
| UI | Jest + RNTL; form, empty/error, erişilebilirlik, tema/i18n |
| Native | Kotlin/Swift service, queue, permission, WidgetKit/Glance |
| E2E | Maestro; manuel işlem, transfer, ödeme, privacy, restore |
| Güvenlik | Key erişimi, log/snapshot leakage, corruption, izin iptali |

%95+ finansal core coverage öneri; tek kalite ölçütü değil, invariants/kritik senaryo zorunlu. CI: format/lint/typecheck/unit/integration/build; iOS macOS/signing. Cihaz matrisi, fixture/CI stratejisi, scriptler pending. Hiçbir uygulama testi çalıştırılmadı.
