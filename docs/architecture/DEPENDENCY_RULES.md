# Bağımlılık kuralları — Accepted (mimari sınırlar)

- @sumlune/core: pure TS, RN/Expo/SQLite/UI/state/ağ/native SDK yok. Saat, kur, ID port/parametre.
- @sumlune/ui: RN ve görsel araçlar; DB/use case/mutasyon yok; formatlanmış veri.
- @sumlune/platform: OS capabilities ve adapter API; mobile feature ve DB doğrudan bağımlılığı yok.
- @sumlune/mobile: composition root, route, feature, adapter; paketleri tüketir. Application domain/port bilir, implementasyon bilmez.
- Feature public index.ts veya açık port; private deep import ve döngü yok.
- Çok modüllü finansal işlem application orkestrasyonu ve tek atomik DB transaction. Dashboard, analytics, widget read-only.
- ESLint import boundary/architecture test önerisi; araç pending.

ADR-0002 onaylıdır; statik analiz aracı ve uygulama ayrıntıları teknik doğrulamaya tabidir. Finansal şema ve double-entry ayrı karardır.
