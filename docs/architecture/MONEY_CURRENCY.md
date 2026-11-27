# Money & Currency Model

ADR-0010 ana kararları Accepted; aşağıdaki ayrıntılar Proposed ve PLAN-03 gözden geçirmesine tabidir.

## Kesin para temsili
Money: currency code + minor unit integer; ISO 4217 exponent 0/2/3 gibi farklı olabilir (JPY/TRY/KWD). UI locale-aware string parse, fazla basamakta açık validasyon; float * 100 yok. Örnek 125,50 TRY → 12550. SQLite signed INTEGER; JS bridge için abs(minor) ≤ 9007199254740991. Girdi, aritmetik ara sonuç, aggregate ve çıkış kontrol edilir. Normal safe integer işlemleri, gerektiğinde BigInt ara hesap; saklama sınırını aşan kayıt sessiz yuvarlanmaz. Öneri: JSON/native sınırında minor unit canonical decimal integer string, adapter güvenli INTEGER'e dönüştürür. Eski kod olmadığı için migration yok. BigInt doğrudan JSON'a verilmez. Decimal.js dönüşüm için, kur TEXT pozitif canonical decimal string. Merkezi rounding önerisi HALF_UP (işaret simetrik, yarımda sıfırdan uzağa), kullanıcı gerçek tahsilatı girdiyse o tutar esas; taksit kalan kuruşu deterministik son takside (PLAN-04). Aynı tutarı tekrar tekrar dönüştürme yok.

## FX
Her rate base/quote, effective date, source (manual/provider), fetched_at ve decimal rate saklar. Otomatik oran referans kurudur, banka gerçekleşme kuru değildir. Manuel rate/tutar override; geçmiş snapshot immutable (düzeltme ayrı revizyon). Varsayılan TRY raporlama değişince orijinal kayıtlar değişmez. Tarihsel gelir/gider tarihsel kurla; mevcut bakiye son bilinen tarihli oranla; eksik dönüşüm açıkça incomplete ve özgün para gösterilir. Güncel kur geçmiş işlemi sessizce yeniden değerlemez. Yeni raporlama para birimi için tarihsel rate yoksa açık eksik durum ve tarihsel lookup/manual; kur uydurma yok.

Önerilen FX posting: her para birimi kendi içinde dengelenir; yalnız farklı döviz transferinde gizli FX clearing sistem hesabı (currency başına). Örnek varsayımsal 3500 TRY → 100 USD, masraf yok: TRY banka -350000 minor, TRY clearing +350000; USD banka +10000, USD clearing -10000. 4 posting tek atomik journal. Gerçek miktarlar ve işlem kuru saklanır. Clearing kullanıcı nakit/gelir/gider/net worth toplamına dahil edilmez; varsa ücret ayrı expense posting. Gerçekleşmiş FX kazanç/vergi muhasebesi onaylı kapsam değil. Kur snapshot ve değerleme testleri gerekir. Dövizli kart alımında gerçek kart borcu para birimi ve özgün alışveriş tutarı ayrı korunur; kesin posting modeli PLAN-03.

## Hibrit kur — Accepted davranış
Manuel giriş offline her zaman çalışır. Uygun ücretsiz servis ile güncel veya tarihsel oran alınabilir; güncel cache tarihli, stale etiketi, uygun tarihi olmayan oranı tarihsel gibi kullanma. Ağ hatası çekirdeği durdurmaz. Öneri: günlük/istek anında cache yenileme, arka plan polling/backend yok. Sağlayıcıya hesap/bakiye/işlem tutarı gönderme. Frankfurter aday (anahtarsız ücretsiz API, referans kurlar; https://frankfurter.dev/); TRY ve gerekli çiftler, lisans/attribution, yanıt hassasiyeti ve hata/limit davranışı entegrasyon öncesi doğrulanacak. Hizmetin gelecekte ücretsiz kalması garanti değil; manuel fallback bağımsız.

## Test adayları
TRY 125.50, JPY 100, KWD 1.234, hatalı input ve max-safe overflow; negatif iade rounding; SQLite/JSON round-trip; FX transferi iki currency dengesi; değişen kur ile geçmiş gider değişmemesi; eksik ve eski kur, raporlama para değişimi; gerçek banka kuru; ücretsiz kaynağın ulaşılamaması.

Referans: https://www.sqlite.org/datatype3.html ve https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER. Teknik kaynaklar kontrol edildi; cihaz, SQLCipher, native bridge ve canlı FX entegrasyonu test edilmedi.
