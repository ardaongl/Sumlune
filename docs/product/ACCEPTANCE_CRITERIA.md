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
| Bütçe geçmiş sürümü | Yeni ay limiti geçmişi değiştirmez. |
| Birikim transferi | Gider yok; aynı bakiye iki kez sayılmaz. |
| Safe-to-spend | Gelecek maaş/limit hariç; overdue ve unassigned debt bir kez; eksik tutar/kur incomplete. |
| 30/60/90 forecast | Aynı seri, gerçekleşen bakiye tekrar sayılmaz, varsayımlar görünür. |
| Önceki dönem 0 veya negatif | Yüzde değişim yok; tutar farkı. |
| Abonelik yıllık maliyeti | Aktif planlar normalize edilir, bilinmeyenler belirtilir. |
| Aynı harcama SMS + bildirim | Çift kayıt yok; belirsiz eşleşme inceleme. |
| İki aynı tutarlı gerçek alışveriş | Weak match ile silme/merge yok; inceleme. |
| İzinli push, açık güvenilir kural | Doğrulanmış gider atomic commit; limit/çakışma/izin hatasında pending. |
| SMS kaynaklı finansal aday | İlk sürüm review-only; izinsiz SMS build yok. |
| Queue retry ve undo | Ack yalnız commit sonrası; replay duplicate değil; undo reversal ve allocation pasifleme. |
| Raw içerik/OTP ve queue overflow | Raw disk/log/network yok; güvenli discard/count, kullanıcı uyarısı. |
| OTP/başarısız işlem | Finansal kayıt yok; hassas içerik saklanmaz. |
| İzin iptali | Manuel ve offline kullanım sürer. |
| Döviz | Orijinal tutar ve kur korunur; eksik kur açıkça gösterilir. |
| Offline | Hesap, işlem ve yerel ödeme sunucusuz çalışır. |
| Widget gizlilik | Masked payload finansal alan içermez; eski snapshot temizlenir, OS reload istenir; anlık launcher cache garantisi yok. |
| Widget midnight/expiry | Eski günlük değer bugün diye sunulmaz; stale placeholder. |
| Widget quick-add / deep link | Auth gate ve açık save; doğrudan finansal yazım yok. |
| Widget publisher privacy race | Eski visible generation maskeli payload üzerine yazamaz. |
| Migration | Önceki kayıtlar korunur, hata güvenli yönetilir. |
| Restore | Hatalı parola/bozuk dosya mevcut veriyi bozmaz. |
| TR/EN ve tema | Kritik akışlarda taşma, okunamaz kontrast, eksik çeviri yok. |

Sayısal performans/kapsam eşikleri teknik aşamada belirlenir. Bunlar test sonucu değildir.
