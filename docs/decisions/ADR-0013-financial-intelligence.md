# ADR-0013 — Financial Intelligence Engine

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi finansal zekâ tasarımını onayladı; teknik ayrıntıları bütçe odaklı olarak asistana devretti.

## Karar
Saf TypeScript hesaplayıcılar ve SQLite read models, budgets/savings_goals tabloları, account spendable ve schedule required flag. Aylık versioned bütçe (rollover yok), gerçek asset hesabına bağlı birikim, 30 günlük varsayılan conservative safe-to-spend (gelecek gelir hariç, borç bir kez, incomplete), planlı 30/60/90 nakit forecast, haftalık/aylık/yıllık analiz, heatmap, dönem kıyası ve normalize abonelik maliyeti. Gerçekleşmiş gider ve cash flow farklı, FX/rounding önceki ADR'lerle uyumlu. Hesaplar ve algoritma [FINANCIAL_INTELLIGENCE](../architecture/FINANCIAL_INTELLIGENCE.md).

## Sonuç
Ek analytics DB, ücretli AI/API, sürekli sunucu, ML tahmini, cache table yok. Uygulama ve cihaz/performans/test doğrulaması henüz yapılmadı. PLAN-05 Smart Capture ayrı teknik karar; kodlama izni yok.
