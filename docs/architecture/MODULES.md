# Modül haritası — Accepted (ana sınırlar)

```text
Sumlune/
  apps/mobile/
    app/                      # Expo Router
    src/
      core/                   # hata, config, localization
      features/               # feature-first
      infrastructure/         # DB, native, security, sync
      providers/              # composition root
    assets/
    app.config.ts
  packages/
    sumlune-core/             # pure TypeScript
    sumlune-ui/               # ortak UI/tokens
    sumlune-platform/         # native contracts/adapters
  docs/
  scripts/
  .github/
  AGENTS.md
  package.json
  pnpm-workspace.yaml
  tsconfig.base.json
```
Bu gelecek scaffold planıdır, oluşturulmadı. Üç ortak paket ve pnpm monorepo onaylıdır; ayrıntılı feature klasörleri ve paket iç yapıları ihtiyaca göre tasarlanır. Eski ledger-* isimleri yerine sumlune-* kullanılır.

| Modüller | Sorumluluk |
|---|---|
| onboarding, dashboard, settings | Kurulum, özet, tercihler |
| accounts, transactions, categories, templates | Hesaplar ve işlem yaşam döngüsü |
| subscriptions, payments, installments, debts, calendar | Yükümlülükler ve ortak recurrence |
| budgets, savings, analytics, forecasting | Read models ve finansal hesaplama |
| smart_capture | Adaylar, parser, otomasyon, dedup |
| widgets, notifications | Snapshot ve platform orkestrasyonu |
| backup, sync | Export, restore, opsiyonel sync |

Feature örneği: domain/, application/, infrastructure/, presentation/, __tests__/, index.ts. İhtiyaç yoksa katman yaratma. Core: money, currencies, accounting, transactions, recurrence, installments, budgeting, forecasting, validation. UI: tokens, themes, primitives, inputs, navigation, finance, charts, feedback, hooks. Platform: capability, capture, widgets, security bridge.
