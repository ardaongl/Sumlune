# Kabul kriterleri — taslak

| Senaryo | Beklenen |
|---|---|
| Bankadan nakde transfer | İki hesap dengeli değişir; gelir/gider değişmez. |
| 500 TL kart harcaması + borç ödeme | Toplam gider 500 TL; ikinci gider yok. |
| Ödeme günü | Harcama oluşmaz; ödenmemiş occurrence görünür. |
| Aynı occurrence aynı komutla iki kez onay | Tek kayıt; idempotent. |
| 31 Ocak aylık plan | Şubat son günü, Mart 31; duplicate occurrence yok. |
| 100 TL / 3 taksit | 33,33 + 33,33 + 33,34 TL; gider alımda bir kez. |
| 500 TL vadenin 200 TL ödemesi | 300 TL kalan; vade geçerse partial + overdue. |
| Ödeme iptali | Reversal ile allocation pasif ve vade yeniden açık. |
| Kart ekstre ve taksit | Aynı principal bir kez planlanır; tek gerçek ödeme kapasitesini aşan allocation reddedilir. |
| Borç alma/verme ve geri ödeme | Anapara gelir/gider değil; faiz ayrı. |
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
