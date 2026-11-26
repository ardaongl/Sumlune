# Güncel durum — 2026-11-26

**Phase:** Planning / Database & Financial Engine. **Coding authorized:** No.

Sumlune, Android/iOS, RN + Expo + TypeScript, Pure Apple, 35 temel özellik + 4 giriş yöntemi, hibrit capture, local-first + opsiyonel bulut, Türkçe docs ve repo tabanlı karar süreci Accepted.

PLAN-00 tamamlandı: baseline commit ae131a0795b3478b829e41516b317c7df088e6f9, 42 Markdown dosyası.
PLAN-01 tamamlandı: Feature-first Modular Monolith, Pragmatic Clean Architecture, Ports & Adapters, pnpm monorepo, üç ortak paket (core/ui/platform) Accepted — ADR-0002. Önerilen teknoloji yığını teknik doğrulama şartıyla Accepted — ADR-0009. Sürümler, SDK/platform uyumu ve aday servislerin nihai seçimi Pending. Double-entry ve tasarım tokenları Proposed; Flutter Superseded.

**Aktif:** PLAN-02: finansal invariants, kayıt modeli (double-entry önerisi), money representation, hesap türleri ve kredi kartı/transfer semantiği. Sonra PLAN-03 ERD/kolon/constraint/migration; PLAN-04 recurrence, kart/taksit/borç/tahmin.

Uygulama kodu, scaffold, paket kurulumu, build ve cihaz testi yok. Private repo hedefi geçerli; görünürlük değişikliği bu oturum kapsamı değildir.

[Backlog](BACKLOG.md) · [Kararlar](DECISION_REGISTER.md) · [Handoff](SESSION_HANDOFF.md).
