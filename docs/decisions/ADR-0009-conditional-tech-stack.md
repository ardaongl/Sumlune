# ADR-0009 — Koşullu teknoloji yığını

**Durum:** Accepted (koşullu)  
**Tarih:** 2026-11-26

## Karar
Ürün sahibi [TECH_STACK](../architecture/TECH_STACK.md) içindeki önerilen yığını teknik uyumluluk doğrulaması şartıyla kabul etti. RN + Expo + TypeScript ve pnpm ana mimari kararları geçerli. Expo development build, Router, Zustand/TanStack Query, expo-sqlite/SQLCipher/Drizzle, form/validation, native Kotlin/Swift/Expo Modules, grafik, bildirim, güvenlik, i18n, test ve build araçları tercih edilen başlangıç adaylarıdır.

## Koşullar
DEV-00 içinde SDK/New Architecture, sürüm/lisans, monorepo autolinking, Android/iOS build, SQLCipher/migration, background capture ve widget entegrasyonu doğrulanmalı. Sonuç ve sürümler dokümante edilir. Başarısızlık halinde ADR ile alternatif ve kullanıcı onayı. Native platform limitleri ortadan kalkmaz. Expo Widgets platform paritesi varsayılmaz; Glance/WidgetKit alternatifleri korunur. Supabase yalnız opsiyonel bulut adayı; E2EE protokolü ve key recovery ayrı karar. Para aritmetiği/persistence temsili PLAN-02'de belirlenir.

## Sonuç
Tercihler kabul edildi; teknik doğrulama yapılmadı. Kodlama, scaffold, kurulum veya build izni verilmedi.
