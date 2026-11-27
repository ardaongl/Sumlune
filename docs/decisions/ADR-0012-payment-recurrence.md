# ADR-0012 — Payment & Recurrence Engine

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi ortak Payment & Recurrence Engine tasarımını onayladı ve açık teknik ayrıntıları bütçe odaklı olarak asistana devretti.

## Karar
Yerel deterministik recurrence, 90 günlük dinamik horizon, tek schedule/occurrence/allocation motoru. Plan ve gerçek journal ayrı; due/notification otomatik gider yaratmaz. Kısmi ödeme, idempotent settlement ve mevcut journal eşleştirme, capacity validation, reversal ile allocation pasifleme. Taksit gideri alımda bir kez, anapara geri ödemesi transfer; kalan kuruş son takside. Kart statement total yerine taksit + non-installment remainder; vade görünümü türetilir, aynı yükümlülük tekrar sayılmaz. Borç/alacak gerçek asset/liability, principal ve faiz ayrı. Yerel hatırlatma, izin/OS limit fallback. Kesin alan ve kurallar [PAYMENT_RECURRENCE](../architecture/PAYMENT_RECURRENCE.md).

## Sonuç
Ayrı ödeme servisi, ücretli API, LLM, sunucu scheduler ve gereksiz subtype tabloları yok. Uygulama, DDL, timezone, native notification ve cihaz testleri yapılmadı. PLAN-04B finansal analiz ve tahmin ayrı karar. Kodlama izni yok.
