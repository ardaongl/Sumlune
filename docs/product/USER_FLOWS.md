# Kullanıcı akışları — Proposed

- İlk açılış: dil/tema → temel para birimi → ilk hesap → özet. Üyelik zorunlu değil; ihtiyaç anında ayrı izin.
- Harcama: Ekle → gider/gelir/transfer → tutar → hesap/kategori → opsiyonel tarih/etiket/açıklama → kaydet → bakiye/snapshot güncelle.
- Şablon: sabit tutar önizleme/onay, değişken tutar girişi; aynı use case.
- Algılama: izinli Android kaynağı → filtre → aday → dedup → kural → kayıt veya inbox. Düzenleme, reddetme, geri alma.
- Ödeme: plan → occurrence → hatırlatma → doğrula veya mevcut işlemle eşleştir → atomik gerçekleşme ve durum.
- Widget: boyut/hesap seç → snapshot → deep link → kilit varsa doğrulama.
- Yedek: kullanıcı başlatır → şifreli yedek → restore önizlemesi → bütünlük kontrolü. CSV/JSON dışa aktarımı yedekten farklıdır.

Ekran sözleşmesi PLAN-08 Proposed: [SCREENS](../design/SCREENS.md), [SCREEN_DETAILS](../design/SCREEN_DETAILS.md).

## Akış karar önerileri
- İlk açılışta 3 kısa adım (dil/tema, rapor currency, ilk hesap/atla/restore); TRY varsayılan; izin isteme ancak ilgili feature açıldığında. Hesap yoksa boş Özet + hesap oluştur; işlem formu hesap gerektirir. Üyelik yok.
- Ekle: default expense ve son başarılı uygun hesap (yoksa seç), currency hesaptan, kategori zorunlu gider/gelir; transfer hedef hesap, farklı currency ise gerçek iki tutar/kur. Tarih bugün, optional detay collapse. Kaydet disabled invalid/submitting, atomic success sonrası kapan ve ilgili liste yenile. Hata formu korur. Şablon seçildiğinde preview; tek tap ile otomatik harcama yok. Hız hedefi 3–5 sn ölçülecek, garanti değil.
- Planlama: tür seç, tutar/değişken, ilk vade/periyot, hesap, reminder, preview; settlement gerçek tutar, kaynak, partial veya mevcut işleme bağla. Vade kendi başına gider değil. Kart alımı/borç anaparası açık semantik. Edit yalnız gelecekteki uygun vadeler; cancel/skip confirmation.
- Capture: Android permission rationale → banka seç/hesap mapping → OS permission → status; review first → explicit rule enable/max limit. Aday edit/approve/link/reject, undo reversal. iOS manual/template. Queue/policy failure açık durum, no fake support.
- Analysis: dönem/filtre, detay drilldown, bütçe ve birikim editor, forecast horizon/expected income toggle, incomplete açıklaması. Safe-to-spend future income hariç.
- Backup: explicit export + passphrase confirmation, file target, başarı durumu; restore preview/replace confirmation/fresh auth/staging. Lock açık widget mask. Cloud ayrı gated phase; conflict iki yedeği koru ve explicit seçim.
