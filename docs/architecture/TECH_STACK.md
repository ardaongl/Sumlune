# Teknoloji yığını

Framework Accepted; aşağıdaki yığın teknik uyumluluk doğrulaması şartıyla Accepted (ADR-0009). Tek tek sürümler ve alternatifler henüz kesinleşmedi. Sürüm/lisans/New Architecture/SDK uyumluluğu başlangıç spike'ında kontrol edilir. Paket kurulmadı; kodlama yetkisi yok.

| Alan | Tercih |
|---|---|
| Mobil | React Native + Expo development builds; Expo Go yeterli değil |
| Dil / workspace | TypeScript strict, pnpm workspaces; Nx/Turborepo yok |
| Navigasyon | Expo Router |
| UI | Sumlune UI kit, StyleSheet; Expo UI/native gerektiğinde |
| State | Zustand UI state, TanStack Query repository sorguları, React hooks |
| Form/validation | React Hook Form, Zod |
| DB | expo-sqlite + SQLCipher, Drizzle ORM/migrations |
| Para | ADR-0010: SQLite INTEGER minor units, JS safe integer; gerektiğinde BigInt, Decimal.js (uyum doğrulaması şartlı); wire ADR-0011 canonical integer-string |
| Native | Expo Modules API, Kotlin, Swift; ADR-0014 foreground drain, WorkManager/Headless JS yalnız ihtiyaç/spike |
| Widget | ADR-0015 Accepted (renderer koşullu): expo-widgets önce uyumluluk spike; SwiftUI/WidgetKit ve Jetpack Glance fallback; ortak snapshot |
| Bildirim | expo-notifications |
| Güvenlik | Expo SecureStore, Expo Local Authentication, OS Keystore/Keychain; ADR-0016 AES-GCM portable backup + PBKDF2-SHA256 (crypto/SDK doğrulama şartlı) |
| UI araçları | Reanimated, Gesture Handler, React Native SVG, Expo Haptics, Lucide React Native |
| i18n | i18next (TR/EN) |
| Bulut | ADR-0016 local encrypted backup first, optional E2EE cloud backup/snapshot CAS sync; Supabase aday |
| Test | Vitest, Jest + React Native Testing Library, Maestro, native test |
| CI/build | GitHub Actions, Expo EAS veya local builds |

SQLite tek kaynak; cache/Zustand yerine geçmez. Config plugin/prebuild ile özel native kaynakların korunması ayrı karar. Expo Widgets iki platformu destekliyor varsayılmaz.

## Referanslar (sonraki doğrulama)
- https://docs.expo.dev/develop/development-builds/introduction/
- https://docs.expo.dev/modules/overview/
- https://docs.expo.dev/versions/latest/sdk/sqlite/
- https://docs.expo.dev/guides/monorepos/
- https://orm.drizzle.team/docs/connect-expo-sqlite
- https://reactnative.dev/docs/headless-js-android

## Doğrulama kapısı (Pending)
- SDK/RN/React/Node/pnpm uyum matrisi, lisanslar, bağımlılık bakım durumu ve lockfile.
- Monorepo autolinking, custom development build, native target/config plugin ve Android/iOS build.
- SQLCipher + Drizzle migration, kesin para serileştirmesi ve anahtar/lifecycle erişimi.
- Android capture izinleri/queue/arka plan, iOS widget extension ve Android Glance, Expo Widgets gerçek destek matrisi.
- Native bildirim, biyometri, güvenli storage ve grafik/gesture entegrasyonu.
- Başarısız doğrulamada bulguyu ve alternatifini ADR ile ürün sahibine sun; sessiz paket değişikliği yok. Supabase aday olarak kalır; aşamalı E2EE backup/sync tasarımı ADR-0016 Accepted, provider/crypto/uygulama doğrulaması Pending. ADR-0010 persistence kararını belirler; adapter round-trip ve kesin wire/FX semantiği doğrulanacak.
