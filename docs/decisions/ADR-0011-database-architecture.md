# ADR-0011 — Database Architecture ve Shared Payment Engine

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi bütçe odaklı çekirdek şema, artımlı migration ve ortak Payment Engine yaklaşımını onayladı; açık kalan çekirdek teknik kararları asistana devretti.

## Karar
Tek şifreli SQLite, Drizzle migration (ADR-0009 koşullu); UUID TEXT, integer minor unit, append reversal/replacement, FK ve unique idempotency, atomic aggregate, derived balances. Kategoriye bağlı teknik hesap, gizli opening equity ve currency başına FX clearing. Tarihsel immutable rate snapshot; HALF_UP, canonical integer-string wire, safe integer kontrolü ve gerektiğinde BigInt. Ayrıntılar [DATABASE](../architecture/DATABASE.md), [MONEY_CURRENCY](../architecture/MONEY_CURRENCY.md).

Ortak ödeme altyapısı abonelik/fatura/kira/recurring/taksit/borç planlarını tekrar kullanır; ödeme planı ve gerçek journal ayrıdır. Kesin recurrence, allocation, taksit ve borç semantiği PLAN-04, taslak [PAYMENT_RECURRENCE](../architecture/PAYMENT_RECURRENCE.md).

## Alternatifler ve sonuç
Ayrı finans backend'i, Redis, broker, event store ve başlangıçta tüm tabloları oluşturmak gereksiz. SQLCipher/Drizzle, exact adapter, migration ve cihaz testleri pending; geliştirme izni yok. Sağlayıcı ve sync sözleşmesi ayrıca belirlenir. 
