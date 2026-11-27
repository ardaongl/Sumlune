# ADR-0014 — Smart Capture Architecture

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi Smart Capture tasarımını onayladı; ilk entegrasyon hedefleri Akbank ve Ziraat Bankası. Teknik ayrıntılar bütçe odaklı olarak asistana devredildi.

## Karar
Android NotificationListenerService öncelikli; Kotlin allowlist/filter/parser, structured encrypted queue (7 gün/500 event), foreground drain, TS dedup/explicit automation. Ham mesaj/OTP persist/log/network yok. Yalnız supported exact push expense, confirmed account/category ve açık max limit kuralı auto; başlangıç review-first. SMS RECEIVE_SMS ayrı izin/installer/Play gate, review-only; notification-only build SMS izni içermez. iOS manual/template. Weak match review, strong reference doğrulama, atomic journal + candidate + allocation, undo reversal. Banka fixture ve cihaz testinden önce destek iddiası yok. [SMART_CAPTURE](../architecture/SMART_CAPTURE.md).

## Sonuç
LLM/API/backend yok; WorkManager/Headless JS yalnız ihtiyaç ve spike. Permission/force-stop/OEM ve SMS policy kısıtları nedeniyle kesintisiz capture garanti değil. Key lifecycle PLAN-07; widget PLAN-06. Kodlama ve teknik test yapılmadı.
