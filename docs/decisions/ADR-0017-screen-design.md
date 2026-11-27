# ADR-0017 — Screen Specifications & Pure Apple UI

**Durum:** Accepted  
**Tarih:** 2026-11-28

Ürün sahibi ekran, navigation, Pure Apple, tokenlar ve ortak bileşenleri onayladı; açık detayları bütçe odaklı asistana devretti.

## Karar
Dört içerik tabı (Overview/Transactions/Planning/Insights), merkez Add sheet, root onboarding/lock/recovery gate, 25 UX ailesi, fixed Overview hierarchy ve ortak list/detail/forms. Ortak StyleSheet token/theme/primitives sumlune-ui; feature-specific editors uygulama modüllerinde. Light/dark/system, TR/EN, iOS system font, Inter Android (lisans/uyum şartlı), WCAG AA contrast verification, 48dp touch, 200% font hedefi, system keyboard, no unnecessary gradients/glass/shadow. Explicit save, no fake financial values, incomplete state, privacy/chart/accessibility masking, cloud phase gate. Küçük dev-only Playground, no mandatory Storybook. [SCREENS](../design/SCREENS.md), [SCREEN_DETAILS](../design/SCREEN_DETAILS.md), [DESIGN_TOKENS](../design/DESIGN_TOKENS.md), [COMPONENTS](../design/COMPONENTS.md), [USER_FLOWS](../product/USER_FLOWS.md) bağlayıcı.

## Sonuç
Onay 35+4 kapsamı korur, gerçek render/Figma/cihaz sonucu değildir. Font/contrast ve native UI teknik gate pending. PLAN-09A Testing & Quality aktif; sonra PLAN-09B phase blueprints/progress. Kodlama yetkisi yok.
