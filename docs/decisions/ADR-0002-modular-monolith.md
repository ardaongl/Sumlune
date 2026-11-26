# ADR-0002 — Feature-first modular monolith

**Durum:** Accepted  
**Tarih:** 2026-11-26  
**Onay:** Ürün sahibi, mimari ve koşullu teknoloji yığını onayı.

## Bağlam
Android/iOS ortak uygulaması, yerel finansal doğruluk, native servis izolasyonu ve uzun vadeli okunabilirlik. Küçük ekip ve Codex oturumları arasında sürdürülebilir bağlam.

## Karar
- Feature-first Modular Monolith; Pragmatic Clean Architecture + Ports & Adapters.
- pnpm workspaces; tek çalıştırılabilir mobil uygulama (`apps/mobile`), üç ortak paket: `packages/sumlune-core` (saf TypeScript finansal domain), `packages/sumlune-ui` (Pure Apple tasarım sistemi), `packages/sumlune-platform` (native sözleşmeler ve adaptörler).
- Domain platformdan ve persistence'tan bağımsız; application use case'ler orkestrasyon yapar; infrastructure port implementasyonları sağlar; presentation iş kurallarını tekrar etmez.
- Feature sınırları public API/port ile korunur; gereksiz katman veya her feature için ayrı workspace yok. Composition root mobil uygulamada.
- Paket ve SDK tercihleri teknik uyumluluk doğrulaması şartıyla kabul edildi; ayrıntılar [ADR-0009](ADR-0009-conditional-tech-stack.md).

## Alternatifler
Tek katmanlı app (sınırlar zayıf), her feature ayrı paket (gereksiz koordinasyon), microservices (kişisel/offline ürün için aşırı karmaşıklık).

## Sonuçlar
Bağımlılık yönleri ve atomik finansal yazım kuralları bağlayıcı; exact finansal veri modeli, double-entry ve para temsili ayrı kararlar. Onay mimarinin uygulandığı veya teknik uyumluluğun ispatlandığı anlamına gelmez. Scaffold ve kodlama yetkisi verilmedi.
