# Kullanıcı akışları — Proposed

- İlk açılış: dil/tema → temel para birimi → ilk hesap → özet. Üyelik zorunlu değil; ihtiyaç anında ayrı izin.
- Harcama: Ekle → gider/gelir/transfer → tutar → hesap/kategori → opsiyonel tarih/etiket/açıklama → kaydet → bakiye/snapshot güncelle.
- Şablon: sabit tutar önizleme/onay, değişken tutar girişi; aynı use case.
- Algılama: izinli Android kaynağı → filtre → aday → dedup → kural → kayıt veya inbox. Düzenleme, reddetme, geri alma.
- Ödeme: plan → occurrence → hatırlatma → doğrula veya mevcut işlemle eşleştir → atomik gerçekleşme ve durum.
- Widget: boyut/hesap seç → snapshot → deep link → kilit varsa doğrulama.
- Yedek: kullanıcı başlatır → şifreli yedek → restore önizlemesi → bütünlük kontrolü. CSV/JSON dışa aktarımı yedekten farklıdır.

Ekran, hata/empty/loading/permission-denied ayrıntıları henüz onaylanmadı.
