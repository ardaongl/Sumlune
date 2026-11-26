# Widget mimarisi — Proposed

Altı tür kapsam Accepted. Akış: SQLite → ortak read model → Widget Snapshot Service → versioned shared storage → native renderer. Android Glance, iOS SwiftUI/WidgetKit; Expo Widgets ancak platform/sürüm doğrulanırsa. Widget DB açmaz, ana anahtar yok, hesaplama tekrarlanmaz. Minimum alan, schemaVersion, üretim zamanı, privacy; kesin alanlar pending. App Group/Android storage güvenliği test. Deep link kilidi atlamaz.

| Tür | İçerik |
|---|---|
| Günlük | Gün toplamı, işlem adedi |
| Yaklaşan ödeme | Tek/çoklu liste, kalan gün, tutar |
| Abonelik | Aylık toplam, aktif adet, sıradaki yenileme |
| Bütçe | Limit, kullanım, kalan |
| Hızlı ekle | İşlem ekranına deep link |
| Bakiye | Seçili hesap/toplam, para birimi |

İşlem commit, plan değişimi, privacy, gün değişimi, app resume invalidation adayları. OS yenileme bütçesi nedeniyle anlık tazelik garanti değil; stale state önerisi. Maske açıksa açık değer yazılmaz ve eski snapshot temizlenir. Boyut, gezinme, veri sözleşmesi ayrı onay.
