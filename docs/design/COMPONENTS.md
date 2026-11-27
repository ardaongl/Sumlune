# UI bileşen envanteri — Proposed

- Primitives: Text, Icon, Surface, Stack, Separator, Pressable, semantic colors.
- Navigation: LargeTitle, TabBar, Header, modal/bottom sheet, context/action menu.
- Inputs: MoneyInput, keypad, Search, Picker, DatePicker, Toggle, category/account selector.
- Finance: BalanceDisplay, TransactionRow, AccountCard, BudgetProgress, PrivacyMask.
- Planning: PaymentRow, SubscriptionRow, Calendar, status indicator.
- Analytics: bar/line/donut/heatmap/progress ring, tooltip ve erişilebilir metin alternatifi.
- Feedback: empty/loading/error/offline/permission denied, confirmation, undo, toast.
- Widget snapshot görünümü ortak token eşlemesiyle native.

Hızlı tab geçişi, bottom sheet, başarılı işlemde hafif haptic, ölçülü bakiye animasyonu, kaydırma/context menu, grafik detay seçimi ve privacy mask. Reduce motion ve erişilebilir alternatif zorunlu hedef. UI Playground development-only; visual regression aday. UI henüz kodlanmadı.

PLAN-08 ortak component contracts: MoneyInput (string, currency, locale, validation, accessible keypad); FinanceAmount (minor string/display, privacy/incomplete); GroupedSection/Row (label, value, icon, trailing action, min touch); FormSheet (safe area, keyboard, dirty discard, pending/submit error); StatusLabel (text+icon, not color-only); EmptyState/InlineError/IncompleteState; PeriodSelector; ChartSummary (accessible data); AuthGate/PrivacyMask; shared PlanEditor/SettlementSheet ve TransactionEditor. Bileşenler domain yazımı yapmaz; props/read models + application callbacks. Yeni component yalnız tekrar kullanım/gerçek ihtiyaç. No custom animation framework.
