# ADR-0018 — Testing & Quality Strategy

**Durum:** Accepted
**Tarih:** 2026-11-28

Ürün sahibi risk odaklı test stratejisi, Quality Matrix ve Definition of Done kurallarını onayladı; açık teknik ayrıntıları bütçe odaklı asistana devretti.

## Karar
Vitest saf core, gerçek SQLite integration ve ayrı SQLCipher native kanıt, Jest/RNTL, Kotlin/Swift, seçili Maestro E2E (stack uyumluluğu şartlı), native gerçek cihaz testleri. Finansal core mevcut modül başına >=95% line, >=90% branch; bütün mandatory davranışlar geçer. 38 Q grubu, P0/P1 fail/blocked/not-run zorunlu gate'i bloke eder. P2 hedef ölçümü/review, P3 minor. Düşük maliyetli local/CI, performans hedefleri ve test edilen SHA'ya bağlı kanıt, kullanıcı faz kabulü; no self-approval. Android/iOS/SMS/cloud platform gate ayrı; hiçbir kanıt uydurulmaz. [TEST_STRATEGY](../engineering/TEST_STRATEGY.md), [QUALITY_MATRIX](../engineering/QUALITY_MATRIX.md), [DEFINITION_OF_DONE](../engineering/DEFINITION_OF_DONE.md) bağlayıcı.

## Sonuç
Araç sürümleri, coverage, test/build/cihaz ve benchmark doğrulanmadı. Kodlama izni yok. PLAN-09B nihai faz blueprint ve progress sistemi hazırlanacak.
