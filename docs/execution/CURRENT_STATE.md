# Güncel durum — 2026-11-28

**Phase:** Planning / Database & Financial Engine. **Coding authorized:** No.

Sumlune, Android/iOS, RN + Expo + TypeScript, Pure Apple, 35 temel özellik + 4 giriş yöntemi, hibrit capture, local-first + opsiyonel bulut, Türkçe docs ve repo tabanlı karar süreci Accepted.

PLAN-00 tamamlandı: baseline commit ae131a0795b3478b829e41516b317c7df088e6f9, 42 Markdown dosyası.
PLAN-01 tamamlandı: Feature-first Modular Monolith, Pragmatic Clean Architecture, Ports & Adapters, pnpm monorepo, üç ortak paket (core/ui/platform) Accepted — ADR-0002. Önerilen teknoloji yığını teknik doğrulama şartıyla Accepted — ADR-0009. Sürümler, SDK/platform uyumu ve aday servislerin nihai seçimi Pending. Lightweight double-entry ve finansal invariants Accepted (ADR-0006, bütçe odaklı devredilmiş karar); tasarım tokenları Proposed; Flutter Superseded. Kapsam değişmedi; kurumsal muhasebe, event sourcing/CQRS, ayrı finans backend'i yok.

PLAN-02 ana kararları tamamlandı: ADR-0010 Money & Currency Accepted; SQLite INTEGER minor units ve JS güvenli sınır, gerektiğinde BigInt, Decimal.js, TRY default/ISO 4217, değiştirilebilir raporlama para birimi, tarihsel kur ve hibrit manuel/ücretsiz otomatik. Kesin sağlayıcı doğrulama bekliyor.

PLAN-03 tamamlandı: ADR-0011 Accepted, tek SQLite, finansal çekirdek, artımlı migration ve ortak ödeme motoru. Devredilmiş teknik seçimler: FX clearing, HALF_UP, canonical integer-string wire, immutable rate snapshot, append reversal/replacement; kesin adapter ve DDL doğrulaması bekliyor.

PLAN-04A tamamlandı: ADR-0012 Accepted, ortak payment/recurrence, 90 günlük horizon, kısmi ödeme, taksit, kart statement remainder, borç/alacak, yerel hatırlatma, allocation kapasitesi ve reversal. Teknik test yok.

**Aktif:** PLAN-04B [Financial Intelligence Engine](../architecture/FINANCIAL_INTELLIGENCE.md) Proposed: aylık bütçe, kategori bütçesi, birikim, safe-to-spend, 30/60/90 nakit akışı, ısı haritası ve analiz. Onaydan sonra PLAN-05 Smart Capture.

Ürün sahibi, teknik kararlar tamamlandığında her faz için ayrı Markdown goal prompt/blueprint ve ilerleme kontrol sistemi istedi. Yürütme gereksinimi [CODEX_EXECUTION_PROTOCOL](CODEX_EXECUTION_PROTOCOL.md) içinde; nihai faz dosyaları PLAN-09'da hazırlanacak.

Uygulama kodu, scaffold, paket kurulumu, build ve cihaz testi yok. Private repo hedefi geçerli; görünürlük değişikliği bu oturum kapsamı değildir.

[Backlog](BACKLOG.md) · [Kararlar](DECISION_REGISTER.md) · [Handoff](SESSION_HANDOFF.md).
