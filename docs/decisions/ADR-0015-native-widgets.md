# ADR-0015 — Native Widget Architecture

**Durum:** Accepted (renderer koşullu)  
**Tarih:** 2026-11-28

Ürün sahibi altı widget, ortak snapshot, small/medium, privacy ve düşük maliyetli platform yaklaşımını onayladı. Teknik ayrıntıları bütçe odaklı olarak asistana devretti.

## Karar
Tek atomic versioned snapshot v1, minimal per-kind data, default masked ve explicit kind consent, global hide override. Scope kind başına, 250 ms normal debounce, privacy immediate generation guard, stale/expiry placeholder, no widget DB/key/direct write/network. Safe allowlisted deep links + auth + explicit save. Önce daily/quick-add, tüm altı tür korunur. Expo Widgets DEV-00 doğrulaması; platform ihtiyacına göre Glance/WidgetKit fallback, tek renderer. [WIDGETS](../architecture/WIDGETS.md) bağlayıcı teknik sözleşme.

## Sonuç
Ek backend/analytics yok; OS refresh ve launcher cache anında silinme garantisi yok. Native SDK, signing, privacy purge ve cihaz doğrulaması pending. Biometric widget consent ayrıntısı PLAN-07. Kodlama yetkisi yok.
