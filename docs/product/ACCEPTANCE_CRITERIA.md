# Kabul kriterleri — taslak

| Senaryo | Beklenen |
|---|---|
| Bankadan nakde transfer | İki hesap dengeli değişir; gelir/gider değişmez. |
| 500 TL kart harcaması + borç ödeme | Toplam gider 500 TL; ikinci gider yok. |
| Ödeme günü | Harcama oluşmaz; ödenmemiş occurrence görünür. |
| Aynı occurrence iki kez onay | Tek kayıt; idempotent. |
| Aynı harcama SMS + bildirim | Çift kayıt yok; belirsiz eşleşme inceleme. |
| OTP/başarısız işlem | Finansal kayıt yok; hassas içerik saklanmaz. |
| İzin iptali | Manuel ve offline kullanım sürer. |
| Döviz | Orijinal tutar ve kur korunur; eksik kur açıkça gösterilir. |
| Offline | Hesap, işlem ve yerel ödeme sunucusuz çalışır. |
| Widget gizlilik | Açık tutar snapshot'ta yok, eski snapshot temizlenir. |
| Migration | Önceki kayıtlar korunur, hata güvenli yönetilir. |
| Restore | Hatalı parola/bozuk dosya mevcut veriyi bozmaz. |
| TR/EN ve tema | Kritik akışlarda taşma, okunamaz kontrast, eksik çeviri yok. |

Sayısal performans/kapsam eşikleri teknik aşamada belirlenir. Bunlar test sonucu değildir.
