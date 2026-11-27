# ADR-0010 — Money & Currency / Hibrit kur

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi önerilen Money & Currency Model ve C hibrit kur sistemini açıkça onayladı.

## Karar
- ISO 4217 para birimleri ve minor unit integer; TRY varsayılan, raporlama para birimi değiştirilebilir. Hesap özgün para birimi, orijinal tutar ve işlem tarihsel kuru korunur.
- SQLite INTEGER, JS güvenli integer sınırı kontrolü; integer aritmetik, gerektiğinde BigInt, Decimal.js ile kur hesabı (paket uyumluluğu ADR-0009). Merkezi finansal yuvarlama politikası.
- Manuel kur desteği öncelikli; ücretsiz bir kaynak doğrulanınca otomatik kur cache'i. Gerçek banka kuru manuel düzeltilebilir. Offline son bilinen kur ve tarihi gösterilir; eksik kur sessizce 1/0 kabul edilmez.
- Ücretli FX API ve zorunlu backend yok. Yerel motor, oran cache'i, minimum network istekleri; yalnız para birimi ve tarih gibi kur sorgusu için gerekli alanlar.
- Otomatik kur sağlayıcısı nihai seçimi, kesin FX clearing, rounding/wire sözleşmesi ve kur provenance ayrıntısı [MONEY_CURRENCY](../architecture/MONEY_CURRENCY.md) taslağında, PLAN-03 içinde netleşecek.

## Alternatifler
Yalnız manuel (ucuz ama sürtünme), yalnız otomatik (offline/gerçek banka kuru sorunları), ücretli API (bütçeye aykırı). Hibrit seçildi. Teknik test/uyum henüz yapılmadı; kodlama yetkisi verilmedi.
