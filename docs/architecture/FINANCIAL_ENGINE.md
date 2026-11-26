# Finansal motor — Proposed; sonraki karar

Double-entry: journal entry + postings, varlık/yükümlülük/gelir/gider/dengeleme hesapları; saf TS. Kullanıcı muhasebe terminolojisi görmez.

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
