# ADR-0019 — Codex Phase Blueprints & Progress Control
**Durum:** Accepted (yürütme gereksinimi kullanıcı onaylı; faz ayrımı devredilmiş teknik planlama).
**Tarih:** 2026-11-28

13 faz, 64 task; 00–09 local-first Android öncelikli, 10 izinli SMS, 11–12 aşamalı cloud. iOS ayrı verification/release lane; kapsam korunur. Her faz bağımsız Markdown goal prompt, task dependencies, scope/UX/Q mapping, test evidence, checkpoint, explicit user acceptance. PROGRESS tek mutable source, no self-approval, P0/P1 mandatory gate, no silent scope changes; reset sayısı faz sayısı değil. START_HERE, MASTER_PLAN, SCOPE_TRACEABILITY, EVIDENCE_TEMPLATE, TECHNICAL_VALIDATION. Ücretli işlem/deploy yok. Bu plan uygulama kodlama yetkisi değildir. Gerçek test ve platform desteği henüz doğrulanmadı.
