# Finansal motor — Lightweight double-entry (Accepted); çekirdek ve ödeme motoru Accepted; analiz Accepted

ADR-0006: Lightweight double-entry; journal entry + postings, varlık/yükümlülük/gelir/gider/dengeleme hesapları; saf TS. Kullanıcı muhasebe terminolojisi görmez. Basit ortak posting builder ve validator, atomik repository. Tam muhasebe sistemi, kullanıcı yönetimli hesap planı, dönem kapatma, resmi raporlama, event sourcing/CQRS veya finans backend'i yok. Bütçe ilkesi: en küçük doğru çözüm; ücretsiz yerel hesaplama; yeni bağımlılık ancak gerekçeli.

| İşlem | Örnek |
|---|---|
| Nakit market 500 TL | Gider +500, nakit -500 |
| Kart market 500 TL | Gider +500, yükümlülük +500 |
| Kart ödeme 500 TL | Banka -500, yükümlülük -500; gider yok |
| Nakit çekme | Banka -500, nakit +500; gider yok |
| Birikim transferi | Kaynak azalır, hedef artar; gider yok |
| İade | Orijinal işlem ilişkili düzeltme; tekrar sayım yok |

ADR-0010 Accepted: minor unit SQLite INTEGER, güvenli JS integer sınırı, gerektiğinde BigInt, Decimal.js ile kur, ISO 4217, TRY varsayılan ve değiştirilebilir raporlama para birimi, tarihsel kur ve hibrit ücretsiz/manuel kaynak. [Money & Currency](MONEY_CURRENCY.md) ayrıntıları; FX posting, HALF_UP yuvarlama ve canonical integer-string wire ADR-0011 ile Accepted. Atomik yazım, idempotency, balanced postings, revizyon/iptal geçmişi. Gerçekleşen zaman UTC + yerel bağlam; planlar yerel takvim/timezone.

Plan occurrence üretir, gerçekleşme ayrı journal entry. Ay sonu, 29 Şubat, DST, partial payment, taksit rounding, kart dönemleri, borç/alacak ADR-0012 Accepted; tahmin ve bütçe ADR-0013 Accepted; iade ve açılış bakiyesi temel kuralları DATABASE içinde Accepted. Kur sağlayıcısı doğrulama bekliyor.

ADR-0013: [FINANCIAL_INTELLIGENCE](FINANCIAL_INTELLIGENCE.md) bağlayıcı. Safe-to-spend operating cash eksi zorunlu vadeler ve plan dışı liability rezervi; gelecek gelir eklenmez, birikim zaten hariç, eksik veri incomplete. Forecast 30/60/90 planlı net nakit, bütçe actual expense postings, normalize abonelik yıllık maliyeti.

## Değişmez kurallar (Accepted)
Dengeli posting, atomik yazım, idempotency, kesin para aritmetiği, izlenebilir edit/iptal, posting kaynaklı bakiye (bağımsız bakiye mutasyonu yok), plan/gerçekleşme ayrımı, deterministik hesap ve platform bağımsızlığı. Aynı para birimi için debit=credit; farklı döviz transferinde currency başına clearing posting (ADR-0011). Basit revizyon/iptal izi yeterli; event sourcing gerekmez. Kredi kartı borcu kredi limiti veya nakit varlık değildir. Finansal testler ve gerçek veri migration koruması sadeleştirme adına kaldırılmaz.

**Sıradaki:** PLAN-05 [Smart Capture](SMART_CAPTURE.md). PLAN-04B Financial Intelligence Accepted. PLAN-03 çekirdek ve PLAN-04A [Payment & Recurrence Engine](PAYMENT_RECURRENCE.md) Accepted; uygulama/test yok.
