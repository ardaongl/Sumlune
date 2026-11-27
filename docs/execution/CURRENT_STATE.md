# Güncel durum — 2026-11-28

**Phase:** Planning / Native Widget Architecture. **Coding authorized:** No.

Sumlune, Android/iOS, RN + Expo + TypeScript, Pure Apple, 35 temel özellik + 4 giriş yöntemi, hibrit capture, local-first + opsiyonel bulut, Türkçe docs ve repo tabanlı karar süreci Accepted.

PLAN-00 tamamlandı: baseline commit ae131a0795b3478b829e41516b317c7df088e6f9, 42 Markdown dosyası.
PLAN-01 tamamlandı: Feature-first Modular Monolith, Pragmatic Clean Architecture, Ports & Adapters, pnpm monorepo, üç ortak paket (core/ui/platform) Accepted — ADR-0002. Önerilen teknoloji yığını teknik doğrulama şartıyla Accepted — ADR-0009. Sürümler, SDK/platform uyumu ve aday servislerin nihai seçimi Pending. Lightweight double-entry ve finansal invariants Accepted (ADR-0006, bütçe odaklı devredilmiş karar); tasarım tokenları Proposed; Flutter Superseded. Kapsam değişmedi; kurumsal muhasebe, event sourcing/CQRS, ayrı finans backend'i yok.

PLAN-02 ana kararları tamamlandı: ADR-0010 Money & Currency Accepted; SQLite INTEGER minor units ve JS güvenli sınır, gerektiğinde BigInt, Decimal.js, TRY default/ISO 4217, değiştirilebilir raporlama para birimi, tarihsel kur ve hibrit manuel/ücretsiz otomatik. Kesin sağlayıcı doğrulama bekliyor.

PLAN-03 tamamlandı: ADR-0011 Accepted, tek SQLite, finansal çekirdek, artımlı migration ve ortak ödeme motoru. Devredilmiş teknik seçimler: FX clearing, HALF_UP, canonical integer-string wire, immutable rate snapshot, append reversal/replacement; kesin adapter ve DDL doğrulaması bekliyor.

PLAN-04A tamamlandı: ADR-0012 Accepted, ortak payment/recurrence, 90 günlük horizon, kısmi ödeme, taksit, kart statement remainder, borç/alacak, yerel hatırlatma, allocation kapasitesi ve reversal. Teknik test yok.

PLAN-04B tamamlandı: ADR-0013 Accepted, local deterministic budgets/savings/safe-to-spend/forecast/analytics; iki yeni tablo, ek sunucu/ücretli AI yok. Teknik detaylar devredilmiş kararla kesinleştirildi; test yok.

PLAN-05 tamamlandı: ADR-0014 Accepted, Akbank ve Ziraat ilk entegrasyon hedefi, notification-first, encrypted structured queue/foreground drain, push expense opt-in auto, SMS ayrı izin ve review-only. Banka desteği, izinler, parser/cihaz testleri pending.

**Aktif:** PLAN-06 [Native Widget Architecture](../architecture/WIDGETS.md) Proposed. Altı home-screen widget, tek privacy-filtered snapshot, Expo Widgets uyumluluk spike ve native fallback; sonra PLAN-07 Security & Cloud Sync.

Ürün sahibi, teknik kararlar tamamlandığında her faz için ayrı Markdown goal prompt/blueprint ve ilerleme kontrol sistemi istedi. Yürütme gereksinimi [CODEX_EXECUTION_PROTOCOL](CODEX_EXECUTION_PROTOCOL.md) içinde; nihai faz dosyaları PLAN-09'da hazırlanacak.

Uygulama kodu, scaffold, paket kurulumu, build ve cihaz testi yok. Private repo hedefi geçerli; görünürlük değişikliği bu oturum kapsamı değildir.

[Backlog](BACKLOG.md) · [Kararlar](DECISION_REGISTER.md) · [Handoff](SESSION_HANDOFF.md).
