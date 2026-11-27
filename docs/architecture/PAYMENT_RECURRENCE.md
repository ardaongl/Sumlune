# Payment & Recurrence Engine — PLAN-04 / Proposed

Ortak ödeme yaklaşımı ADR-0011 ile Accepted; aşağıdaki davranış/şema önerisi onay bekliyor. Yerel saf TS recurrence hesaplayıcı, SQLite plan/occurrence/allocation, mevcut finansal motor. Ödeme takibi banka üzerinden para göndermek değildir. Ek backend, scheduler servisi veya LLM yok.

## Ortak yaşam döngüsü
Schedule (kural) → occurrence (beklenen vade) → kullanıcı onayı veya güvenilir capture ile journal (gerçekleşme) + allocation. Vade/notification tek başına gider yaratmaz. Durumlar: pending, partial, settled, skipped, cancelled; overdue yerel tarihte vade < bugün ve kalan > 0 olduğunda türetilir. Partial + overdue birlikte olabilir. Pause/cancel geçmişi silmez; gelecekteki ödenmemiş occurrence'lara açık işlem. Geçmiş vade değişikliği sessizce yapılmaz. Actual amount planla farklıysa kullanıcı gerçek tutarı onaylar ve farkı kaydeder veya planı günceller; otomatik olarak sessiz kapanmaz.

## Tekrar kuralları
Once, weekly, monthly, yearly ve pozitif interval (ör. 3 ay); gerekirse belirli son tarih/adet. Original anchor day saklanır; kısa ayda son gün, sonraki uzun ayda asıl gün (31 Ocak → 28/29 Şubat → 31 Mart). Ayın son günü ayrı anchor mode; 29 Şubat yıllık aynı prensip. Yerel takvim günü ve IANA timezone, hatırlatma saati ayrı; DST nonexistent → sonraki geçerli saat, ambiguous → ilk oluşum (test). App açılış/foreground ve plan değişikliğinde bounded rolling horizon (öneri 90 gün) üret; uzun offline aralıkta kontrollü batch ile kaçırılan vadeleri geri kazan; takvim ileri gezilirse on-demand. UNIQUE(schedule_id, occurrence_key) ve idempotent generation. Güncelleme yalnız gelecekteki henüz ödenmemiş planlara; tarihsel/partial/settled korunur, aynı vade iki kez oluşmaz.

## Türlere göre finansal semantik
| Tür | Plan | Gerçekleşme |
|---|---|---|
| Subscription / bill / rent / recurring | Sabit/değişken beklenen tutar; recurrence | Gerçek gider veya gelir onaylandığında journal; mevcut işleme bağlama da mümkün |
| Taksitli kart alımı | Satın alım anında tam tutar gider + kart borcu; vade/taksit planı nakit yükünü gösterir | Kart ödemesi liability azaltan transfer; taksit occurrence'ı ikinci gider değildir |
| Nakit taksitli alım / finansman | Alımda tam gider ve payable liability (peşinat varsa ayrı posting); ödeme planı | Anapara borç azaltır, gerçek faiz/ücret gider |
| Borç alma | Banka/nakit artar, payable liability artar | Anapara ödemesi transfer; faiz varsa gider |
| Borç verme | Nakit azalır, receivable asset artar | Anapara geri dönüşü gelir değil; faiz varsa gelir |
| Önceden var olan borç/alacak | Açılış equity karşı kaydı; geçmiş gelir/gider yaratmaz | Anapara hareketleri aynı kurallar |

Taksit örneği: 12.000 TRY / 6 ay = 2.000 TRY aylık plan, alımda 12.000 TRY gider ve borç; aylık ödemede 2.000 TRY borç azalır, yeni gider yok. 100 TRY / 3 = 33,33 + 33,33 + 33,34; minor unit kalan son taksite; toplam tam eşit. Kart taksitinde aynı borcu kart hesap bakiyesi ve taksit toplamı olarak iki kez rezerv etme. Kart ekstresi vadesi/ödeme planı ile taksitler aynı liability üzerinden ilişkilendirilir. Kart kesim/son ödeme günü kullanıcı girer; banka ekstresi içe aktarma veya faiz otomatik tahmini yok. Ödeme ataması kullanıcı onayı veya açık, tekil eşleşme; manuel ödeme tutarı birden fazla taksit/borca bölünebilir. Ödeme allocation ilişkisi kesinleştirildiğinde kart vadesi ve nakit tahmini çifte sayılmaz.

## Önerilen tablo sözleşmesi
- payment_schedules: id, kind, title, currency_code, expected_amount_minor nullable (değişken tutar), source_account_id nullable, target_account_id nullable, category_id nullable, obligation_account_id nullable, origin_journal_id nullable, frequency, interval, start_date, anchor_mode, anchor_day, end_date nullable, occurrence_count nullable, timezone, reminder_offset_days nullable, status, created_at, updated_at. Bütün türlerde aynı tablo; tür bazlı validasyon. Ayrı installment/debt tabloları yalnız gerçek gerekçe ile.
- payment_occurrences: id, schedule_id FK, occurrence_key, due_date, expected_amount_minor nullable, currency_code, resolution_state nullable (skip/cancel), created_at, updated_at. Unique(schedule_id,occurrence_key). Kalan ve paid/partial/overdue durumu allocation'lardan türetilir.
- payment_allocations: id, occurrence_id FK, journal_entry_id FK, amount_minor positive, currency_code (occurrence ile aynı), idempotency_key unique, created_at. Çoklu journal/occurrence; allocation aynı gerçek ödeme kapasitesini aşmaz. Cross-currency settlement gerçek tutar/kur ile dönüştürülür; ödeme kaynağındaki kapasiteyi kontrol etmek için source_minor/source_currency ve rate snapshot gerekirse ekle. Şema detayları onay bekliyor.
- Yeni gerçekleşme ve allocation tek DB transaction; mevcut işleme eşleştirme yeni posting yaratmaz. Reversal/iptal allocation etkisini aynı transaction'da kaldırır/tersler, gerekirse occurrence yeniden açılır; replacement otomatik reallocation yalnız doğrulanmış semantikle. Kısmi ödeme kullanıcı onayıyla, fazla tutar ayrı işlem/explicit plan düzeltmesi; sessiz over-allocation yok. Değişken tutar önce gerçek toplamla doğrulanır.

## Bildirim ve takvim
Yerel bildirim, kullanıcı ayarlı vade öncesi/günü; izin yoksa takvim/in-app görünüm. Yakın zaman penceresi içinde OS kapasitesine göre sınırlı planlama, deterministic notification ID, plan değişimi/ödeme/iptalde cancel/reschedule. App resume reconciliation; exact-time ve teslim garantisi yok. Privacy mask; kilit ekranında varsayılan hassas tutar göstermeme önerisi. Takvim ve widget occurrence read model'i kullanır; ayrı tablo gereksiz.

## Finansal analizle sınır
Gerçek gider = posting; ödenmemiş plan = tahmini gelecekteki cash flow. Abonelik yıllık maliyet normalize periyot ve currency; aktif/paused ayrımı. Kart borcu ve taksit schedule tek yükümlülük olarak sayılır. Safe-to-spend, bütçe ve forecast ayrıntıları Financial Intelligence alt adımında.

## Örnek testler
31 Ocak/Şubat/Mart ve leap year; timezone/DST; tekrar generation, uzun offline; pause/cancel; vade tek başına posting yok; sabit/değişken ücret; duplicate settlement; kısmi/çoklu ödeme; reversal/reopen; taksit kuruşu, kart alımı + ödeme gideri bir kez; borç/alacak principal ve faiz; FX ödeme; kart bakiye ve taksit double count; bildirim izin/yeniden planlama. Hiçbiri henüz çalıştırılmadı.
