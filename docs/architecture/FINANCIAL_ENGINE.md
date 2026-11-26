# Finansal motor — Lightweight double-entry (Accepted); detaylar Pending

ADR-0006: Lightweight double-entry; journal entry + postings, varlık/yükümlülük/gelir/gider/dengeleme hesapları; saf TS. Kullanıcı muhasebe terminolojisi görmez. Basit ortak posting builder ve validator, atomik repository. Tam muhasebe sistemi, kullanıcı yönetimli hesap planı, dönem kapatma, resmi raporlama, event sourcing/CQRS veya finans backend'i yok. Bütçe ilkesi: en küçük doğru çözüm; ücretsiz yerel hesaplama; yeni bağımlılık ancak gerekçeli.

| İşlem | Örnek |
|---|---|
| Nakit market 500 TL | Gider +500, nakit -500 |
| Kart market 500 TL | Gider +500, yükümlülük +500 |
| Kart ödeme 500 TL | Banka -500, yükümlülük -500; gider yok |
| Nakit çekme | Banka -500, nakit +500; gider yok |
| Birikim transferi | Kaynak azalır, hedef artar; gider yok |
| İade | Orijinal işlem ilişkili düzeltme; tekrar sayım yok |

Binary float yok; minor unit integer ve decimal dönüşüm. Orijinal kur/para/tarih saklanır. SQLite INTEGER/JS safe integer/JSON BigInt için temsil ADR gerekli. Atomik yazım, idempotency, balanced postings, revizyon/iptal geçmişi. Çoklu döviz ortak değerleme/FX farkı pending. Gerçekleşen zaman UTC + yerel bağlam; planlar yerel takvim/timezone.

Plan occurrence üretir, gerçekleşme ayrı journal entry. Ay sonu, 29 Şubat, DST, partial payment, taksit rounding, kart dönemleri, borç/alacak, kur kaynağı, net iade, açılış bakiyesi pending.

Güvenle harcanabilir: likit bakiye eksi seçilen ufuktaki ödenmemiş zorunlu yükümlülükler; gelecekteki gelir, kart çifte sayım, birikim rezervi, negatif ve eksik kur politikası pending. 30/60/90 tahmin varsayımları görünür; yıllık abonelik maliyeti normalize periyot ve kur, hesap politikası pending.

## Değişmez kurallar (Accepted)
Dengeli posting, atomik yazım, idempotency, kesin para aritmetiği, izlenebilir edit/iptal, posting kaynaklı bakiye (bağımsız bakiye mutasyonu yok), plan/gerçekleşme ayrımı, deterministik hesap ve platform bağımsızlığı. Aynı para birimi için debit=credit; farklı dövizlerde kesin değerleme/dengelenme politikası sonraki kararda. Basit revizyon/iptal izi yeterli; event sourcing gerekmez. Kredi kartı borcu kredi limiti veya nakit varlık değildir. Finansal testler ve gerçek veri migration koruması sadeleştirme adına kaldırılmaz.

**Sıradaki:** Money & Currency Model; minor units, güvenli integer sınırı, SQLite/JSON temsili, FX/rounding. Bu seçim henüz yapılmadı.
