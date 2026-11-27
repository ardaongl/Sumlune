# Screen Specifications — PLAN-08 / Accepted (ADR-0017)

Pure Apple yönü ADR-0004 Accepted; ekran, token ve bileşen sözleşmesi ADR-0017 ile Accepted. Tüm 35 özellik + 4 giriş yöntemi korunur. Bu dosya navigasyon/ekran haritası, [SCREEN_DETAILS](SCREEN_DETAILS.md) ekran davranış sözleşmesi, [USER_FLOWS](../product/USER_FLOWS.md) akışlar; [DESIGN_TOKENS](DESIGN_TOKENS.md) ve [COMPONENTS](COMPONENTS.md) görsel temel. Gerçek tasarım/render/kod yok.

## Navigation
Dört içerik tabı + ortada Ekle aksiyonu; Expo Router. Ekle tab stack değildir, ortak form sheet açar. Safe area, native back/gesture, restore tab selection; Android/iOS aynı IA. Üst alan sağ: inbox badge (yalnız pending ve privacy uygun) ve settings; hesaplar Özet bakiye alanı üzerinden. Deep link route allowlist + UUID + auth; unknown fallback. Lock/onboarding root gate, sensitive screen flash yok.

| Konum | Route (sözleşme) | Ana iş |
|---|---|---|
| Özet / Overview | /(tabs)/overview | Serbest bakiye, safe-to-spend, aylık harcama, yaklaşan ödeme, son işlem |
| İşlemler / Transactions | /(tabs)/transactions | Tarihe göre liste, arama, filtre, detay |
| Ekle / Add | /transaction/new | Ortak expense/income/transfer sheet; şablon |
| Planlama / Planning | /(tabs)/planning | Takvim ve ödeme yükümlülükleri, abonelik, taksit, borç/alacak |
| Analiz / Insights | /(tabs)/insights | Dönem analizi, bütçe, birikim, forecast, heatmap |

## Ekran envanteri (route family, kesin dosya isimleri blueprint'te)
| ID | Ekran / yüzey | Giriş |
|---|---|---|
| UX-01 | İlk açılış, dil/tema, rapor currency, ilk hesap veya atla/restore | Root |
| UX-02 | Lock / recovery | Root gate |
| UX-03 | Overview | Tab |
| UX-04 | Hesap listesi ve hesap detayı | Overview |
| UX-05 | Hesap create/edit/opening/archiving, kart ayarları | Hesaplar |
| UX-06 | İşlem listesi, search/filter | Tab |
| UX-07 | İşlem create/edit (expense/income/transfer), FX, template | Add/detail |
| UX-08 | İşlem detayı, düzeltme/iptal/iade | Liste |
| UX-09 | Kategori/etiket ve şablon yönetimi | Settings/Add |
| UX-10 | Planning hub ve finansal takvim | Tab |
| UX-11 | Abonelik/fatura/kira/recurring list/detail/create | Planning |
| UX-12 | Taksit list/detail/create, kart ekstre/vade | Planning |
| UX-13 | Borç/alacak list/detail/create | Planning |
| UX-14 | Vade detayı, settlement, partial/link existing | Planning |
| UX-15 | Insights dönem ekranı, kategori dağılımı, heatmap/drilldown | Tab |
| UX-16 | Bütçeler list/detail/editor | Insights |
| UX-17 | Birikim hedefleri list/detail/editor | Insights |
| UX-18 | 30/60/90 forecast ve safe-to-spend detay | Overview/Insights |
| UX-19 | Capture inbox/detail/review | Header (Android capability) |
| UX-20 | Capture setup, bank mapping, automation rules | Settings/Inbox |
| UX-21 | Settings hub, dil/tema/currency/kur/privacy | Header |
| UX-22 | Widget ayarları ve kurulum yardımı | Settings |
| UX-23 | Güvenlik, app lock, permission ve notification settings | Settings |
| UX-24 | Backup/restore/export, recovery | Settings/Root |
| UX-25 | Optional cloud backup/auth/sync/conflict | Settings (yalnız ayrı cloud fazında) |

25 aile; her biri bağımsız ekran olmak zorunda değil. Ortak list/detail/editor ve reusable sheet; gereksiz route duplication yok. Plan türleri aynı form altyapısı; farklı label/validation. Analytics tek motor. Widget ayrı home-screen yüzeyi ADR-0015. No web UI, no extra features.

## Ekran kuralları
- Scroll large title, grouped list, 20 dp padding, semantik tutarlar, tabular numbers, light/dark/system, TR/EN. Default system font iOS, Inter Android tercih (lisans/cihaz doğrulaması şartlı); token contrast validation zorunlu. No neon/gradient/dekoratif glass; animasyon işlevsel.
- Her veri ekranı loading/empty/error/incomplete/locked/privacy (uygun olan) state; offline normal kullanım, network hata yalnız kur/cloud alanında. Financial zero gerçek sıfır ise; eksik veri placeholder + gerekçe. Success sadece commit sonrası; retry idempotent. Destructive confirmation; no optimistic financial truth.
- Money input string, currency exponent/decimal locale; 48dp touch, font scale, screen reader, reduce motion, keyboard/safe area. Chart accessible list/summary. Renk tek anlam taşıyıcı değil. Platform capability false ise açıklayıcı disabled/hidden action, iOS capture özelliği vaat edilmez.
- UI route/feature erişimi auth gate'ten geçer; no raw capture/secret in UI/log. Restore ve lock widget mask; deep link doğrudan kayıt yapmaz. Global hide miktarları UI'da maskele, accessible labels de hassas tutarı ifşa etmez.
- İlk kullanılabilir core yerel; cloud UI only gated phase, fake button/coming soon zorunlu değil. Her faz gerçek çalışan dikey dilim. Design Playground dev-only, fixture sentetik. PLAN-08 onaylandı; uygulama kodu yok.

## Kesin uygulama sınırları
- Root gate: boot/migration → recovery veya onboarding → auth (etkinse) → tabs. Deep link bekleyen hedefi yalnız başarılı gate sonrası açar. React Navigation/Expo Router route group URL parçası değildir; internal group yolları yukarıda, external URI allowlist semantic route olarak çözülür. Ekle ortak modal/sheet; kapanınca önceki tab/scroll korunur; Android back ve iOS dismiss dirty confirmation. Tab bar 4 içerik + merkez aksiyon, Ekle seçili kalıcı sekme değil.
- Overview fixed hierarchy; toplam serbest bakiye ve net worth aynı metrik değildir; ilk 3 açık ödeme/son 5 actual işlem. Capture inbox yalnız Android capability; settings tüm root tablardan erişilebilir. Cloud UI yalnız kendi fazında. Gerçekten hazır olmayan feature için sahte işlev yok; faz tamamlanana dek kontrollü capability gate. 25 aile route sayısı hedefi değil; reusable screen/feature form.
- UX-07 amount-first, sistem klavyesi varsayılan; custom keypad başlangıçta şart değil. No default category guessing; son başarılı uygun hesap, tarih bugün, optional details collapsed. Global privacy chart/progress ve amount accessibility labels dahil finansal değerleri gizler; açık edit sırasında gerekli tutar girişi kullanıcı eylemiyle görünür, kilit gate korunur. No custom dashboard. Tasarım tokenları ve state testleri PLAN-09A. 
