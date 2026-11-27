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
| Pure Apple tokenlar, 4 tab + Ekle, 25 ekran ailesi, ortak UI, Inter (lisans/cihaz şartlı) | Accepted | ADR-0017 / DESIGN_SYSTEM |
| İngilizce kod, main, Conventional Commits | Proposed | GIT_WORKFLOW |
| Smart Capture notification-first, encrypted queue, foreground drain, gated SMS/review, Akbank ve Ziraat ilk hedef | Accepted | ADR-0014 / SMART_CAPTURE |
| Banka fixture, izin ve cihaz doğrulaması | Pending | SMART_CAPTURE / DEV-00 |
| Altı widget, ortak snapshot v1, privacy default masked, deep link, small/medium | Accepted | ADR-0015 / WIDGETS |
| Widget renderer, SDK ve cihaz doğrulaması | Pending | ADR-0015 / DEV-00 |
| Money & Currency: minor units, güvenli INTEGER, TRY varsayılan, ISO 4217, değiştirilebilir raporlama, tarihsel kur, hibrit ücretsiz/manuel | Accepted | ADR-0010 / MONEY_CURRENCY |
| FX clearing, HALF_UP, canonical integer-string wire, immutable rate snapshot | Accepted (devredilen teknik seçim) | ADR-0011 / MONEY_CURRENCY |
| Ücretsiz kur sağlayıcısı ve adapter doğrulaması | Pending | MONEY_CURRENCY |
| Tek SQLite, çekirdek şema, artımlı migration, ortak Payment Engine | Accepted | ADR-0011 / DATABASE |
| Payment/recurrence/taksit/borç detayları, 90 günlük horizon, kısmi ödeme | Accepted | ADR-0012 / PAYMENT_RECURRENCE |
| Bütçe, birikim, safe-to-spend, nakit tahmini ve analiz | Accepted | ADR-0013 / FINANCIAL_INTELLIGENCE |
| Yerel güvenlik, portable encrypted backup, C aşamalı cloud backup ve CAS snapshot sync | Accepted | ADR-0016 / SECURITY / SYNC |
| Crypto/SDK, provider/kota/RLS ve cihaz doğrulaması | Pending | ADR-0016 / DEV-00 ve cloud fazı |
| Ekran detayları, navigation, component/token sözleşmesi | Accepted | ADR-0017 / SCREENS |
| Risk temelli test, coverage, kalite kapısı ve cihaz matrisi | Proposed | TEST_STRATEGY / QUALITY_MATRIX / PLAN-09A |
| Flutter ve eski Dart stack | Superseded | ADR-0008 |

[ADR dizini](../decisions/INDEX.md). Yeni karar kabul edilince ilgili ADR ve tüketen dokümanlar birlikte güncellenir; eski karar silinmez, superseded işaretlenir.
