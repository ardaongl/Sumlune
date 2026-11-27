# Karar kayıt defteri

Accepted yalnız açık onay; Accepted (koşullu) = tercih onaylı, teknik doğrulama bekliyor; Proposed teknik öneri; Pending çözülmemiş; Superseded eski karar. Baseline: 2026-11-26.

| Karar | Durum | Kaynak |
|---|---|---|
| Sumlune adı, private repo hedefi, Türkçe doküman | Accepted | ADR-0007 |
| Android + iOS | Accepted | PRD / ADR-0001 |
| RN + Expo + TypeScript | Accepted | ADR-0001 |
| 35 özellik + 4 giriş yöntemi | Accepted | SCOPE |
| Hibrit otomatik kayıt | Accepted | ADR-0005 |
| Local-first + opsiyonel bulut | Accepted | ADR-0003 |
| Pure Apple | Accepted | ADR-0004 |
| Kodlama yok, kararlar repo üzerinden | Accepted | ADR-0007 |
| Teknik kararlar tamamlandıktan sonra her geliştirme fazına ayrı Markdown goal prompt/blueprint ve ilerleme kontrol sistemi | Accepted | CODEX_EXECUTION_PROTOCOL |
| Feature-first modular monolith, Pragmatic Clean Architecture, Ports & Adapters, 3 paket, pnpm | Accepted | ADR-0002 |
| Lightweight double-entry ve finansal invariants | Accepted (ürün sahibi seçimi devretti) | ADR-0006 |
| Bütçe ilkesi: en küçük doğru çözüm, gereksiz altyapı yok; onaylı kapsam korunur | Accepted (yönlendirme) | ADR-0006 |
| Önerilen teknoloji yığını (SQLCipher, Drizzle, Zustand, TanStack Query, native stack dahil) | Accepted (koşullu) | ADR-0009 / TECH_STACK |
| Paket sürümleri, platform uyumu, Expo Widgets desteği, Supabase nihai seçimi | Pending | TECH_STACK / ADR-0009 |
| Tokenlar, ekran haritası, Inter | Proposed | DESIGN_SYSTEM |
| İngilizce kod, main, Conventional Commits | Proposed | GIT_WORKFLOW |
| Capture ve widget sözleşmeleri | Pending | SMART_CAPTURE / WIDGETS |
| Money & Currency: minor units, güvenli INTEGER, TRY varsayılan, ISO 4217, değiştirilebilir raporlama, tarihsel kur, hibrit ücretsiz/manuel | Accepted | ADR-0010 / MONEY_CURRENCY |
| FX clearing, HALF_UP, canonical integer-string wire, immutable rate snapshot | Accepted (devredilen teknik seçim) | ADR-0011 / MONEY_CURRENCY |
| Ücretsiz kur sağlayıcısı ve adapter doğrulaması | Pending | MONEY_CURRENCY |
| Tek SQLite, çekirdek şema, artımlı migration, ortak Payment Engine | Accepted | ADR-0011 / DATABASE |
| Payment/recurrence/taksit/borç detayları, 90 günlük horizon, kısmi ödeme | Accepted | ADR-0012 / PAYMENT_RECURRENCE |
| Bütçe, birikim, safe-to-spend, nakit tahmini ve analiz | Proposed | FINANCIAL_INTELLIGENCE / PLAN-04B |
| E2EE, backup, conflict | Pending | SECURITY / SYNC |
| Flutter ve eski Dart stack | Superseded | ADR-0008 |

[ADR dizini](../decisions/INDEX.md). Yeni karar kabul edilince ilgili ADR ve tüketen dokümanlar birlikte güncellenir; eski karar silinmez, superseded işaretlenir.
