# Ürün gereksinimleri (PRD)

[SCOPE](SCOPE.md) bağlayıcıdır. Aşağıdaki davranışlar taslak kabul kriterleridir; teknik ayrıntılar ayrıca onaylanır.

| ID | Alan | Gereksinim |
|---|---|---|
| FIN-01 | Hesap | Nakit/banka/kart, açılış bakiyesi, hesap para birimi; kart borcu varlık değildir. |
| FIN-02 | İşlem | Gider, gelir, transfer; tarih, hesap, tutar, kategori, etiket, açıklama. |
| FIN-03 | Kur | Orijinal döviz ve işlem kuru saklanır; farklı dövizler doğrudan toplanmaz. |
| PLN-01 | Ödeme | Plan ve gerçekleşme ayrı; bekleyen/ödenen/geciken; doğrulama veya uygun otomasyon. |
| PLN-02 | Abonelik | Sonraki yenileme, periyot, aylık/yıllık maliyet, aktif/durdurulmuş durum. |
| PLN-03 | Yükümlülük | Kira/fatura/taksit/borç/alacak, takvim ve hatırlatma. |
| INT-01 | Bütçe | Aylık/kategori limit, kalan tutar, dönem karşılaştırması. |
| INT-02 | Birikim | Hedef ve ilerleme; transfer gider değil. |
| INT-03 | Tahmin | Güvenle harcanabilir ve 30/60/90 günlük tahmin; varsayımları göster. |
| INT-04 | Analiz | Haftalık/aylık/yıllık grafik, ısı haritası, tutarlı filtre/kur. |
| CAP-01 | Manuel | Hızlı tutar girişi; sabit/değişken şablon ve önceden seçilmiş alanlar. |
| CAP-02 | Algılama | Açık izinli Android kaynakları; aday, dedup, gelen kutusu. |
| CAP-03 | Hibrit | Önce onay, yalnız etkinleştirilmiş güvenilir kural otomatik kayıt. |
| WID-01 | Widget | Altı tür, gizlilik, deep link, OS yenileme kısıtları. |
| SEC-01 | Güvenlik | Biyometrik kilit, maskeleme, güvenli veri saklama. |
| DAT-01 | Veri | Offline, backup/restore, CSV/JSON export, opsiyonel bulut. |
| UX-01 | UX | Pure Apple, light/dark/system, TR/EN, erişilebilirlik. |

Kişisel finans takibi; banka hesabından ödeme gönderme veya banka kimlik bilgisi yönetimi değil. Banka bildirimi mutabakat garantisi değil. Tahmin finansal garanti değil. iOS'ta üçüncü taraf SMS/bildirim capture paritesi vaat edilmez.
