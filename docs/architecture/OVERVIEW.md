# Teknik mimari

Accepted: React Native + Expo + TypeScript, Android/iOS, local-first, Pure Apple, hibrit capture. Accepted (ADR-0002): feature-first modular monolith, ports & adapters, pragmatik Clean Architecture, pnpm monorepo ve üç ortak paket. Teknoloji yığını ADR-0009 uyarınca koşullu Accepted; teknik doğrulama bekliyor. Flutter superseded.

```mermaid
flowchart TD
  UI[Presentation / Expo Router] --> APP[Application / use cases]
  APP --> CORE[Pure TypeScript finance domain]
  APP --> PORT[Repository & platform ports]
  INF[Infrastructure adapters] --> PORT
  INF --> DB[(SQLite)]
  INF --> NATIVE[Kotlin / Swift]
  INF --> CLOUD[Optional cloud]
```
Domain saf iş kuralları; application orkestrasyon; presentation ekran/hook/UI state; infrastructure persistence, native, network. Tek uygulama, tek finansal veri kaynağı. Microservice, gereksiz abstraction veya her feature için ayrı workspace yok. Mobile composition root DI ve adapter wiring. Native olay yakalar, ortak motor kayıt oluşturur; widget snapshot okur. Bulut kapalıyken temel deneyim devam eder. İlk spike: native lifecycle, SQLCipher, widget target ve background erişimi. Henüz test edilmedi.

Lightweight double-entry Accepted (ADR-0006); kesin para ve veri modeli Pending (PLAN-02/03). Kısıtlı bütçe için en küçük doğru çözüm, harici finans backend'i/event sourcing/CQRS yok. Mimari onayı kodlama izni değildir.
