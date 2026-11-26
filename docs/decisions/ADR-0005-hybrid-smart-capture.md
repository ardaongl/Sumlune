# ADR-0005 — Hibrit harcama otomasyonu

**Durum:** Accepted  
**Tarih:** 2026-11-26

## Bağlam ve karar
Manuel ve şablon iki platform, Android SMS/bildirim. Önce tüm adaylar onay; yalnız kullanıcının etkinleştirdiği güvenilir kurallar otomatik.

## Alternatifler
Her zaman onay, doğrudan otomatik kayıt.

## Sonuçlar ve sınırlar
İzin/policy, dedup, güvenlik, queue, parser ve geri alma tasarımı gerekir.
