# ADR-0016 — Security & Phased Cloud Sync

**Durum:** Accepted (teknik doğrulama şartlı)  
**Tarih:** 2026-11-28

Ürün sahibi Security Architecture ve C aşamalı bulut entegrasyonunu onayladı; teknik ayrıntıları bütçe odaklı asistana devretti.

## Karar
SQLCipher + random device key, ayrı biometric UI gate; lock açıkken widget masked. Portable versioned AES-256-GCM backup, PBKDF2-SHA256 başlangıç tercihi doğrulama şartlı, user passphrase, no raw/keys, crash-safe staged restore ve explicit replace. CSV/JSON explicit plaintext export. Önce local, sonra optional encrypted cloud backup, sonra optional CAS snapshot sync; Supabase aday, provider/kota/RLS doğrulaması şartlı. Çakışmada iki versiyon korunur ve explicit seçim; no silent LWW/row merge. Cloud local release blocker değil; kapsamdan çıkarılmadı.

## Sonuç
[SECURITY](../architecture/SECURITY.md), [SYNC](../architecture/SYNC.md) bağlayıcı. No mandatory server/paid upgrade. Crypto/SDK/cihaz, restore, RLS ve CAS testleri zorunlu; yapılmadı. Kodlama yetkisi yok. PLAN-08 ekran tasarımı aktif.
