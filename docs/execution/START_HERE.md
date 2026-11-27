# Codex başlangıç ve devam rehberi
Kodlama yetkisi henüz No. Güncel main'i local clone/pull (dirty worktree varsa önce kullanıcı değişikliklerini koru); repo private hedefi, public risk R-01; gerçek veri/secret hiçbir zaman Git'e. Uygun yerel Codex workspace olarak repo root aç. İlk yeni oturumda yalnız şu talimatı ver:

> Sumlune repository'sinde AGENTS.md ve docs/execution/START_HERE.md oku. docs/execution/phases/PHASE-00-TECHNICAL-VALIDATION.md goal prompt'unu çalıştırmanı açıkça onaylıyorum. Yalnız bu fazı uygula; PROGRESS ve kanıtları güncelle, kalite kapısından sonra dur ve benim onayımı bekle. Ücretli işlem, deployment veya başka faz yok.

Sonraki oturum (aynı faz):
> AGENTS.md, CURRENT_STATE.md, PROGRESS.md, SESSION_HANDOFF.md ve aktif PHASE-XX dosyasını oku. Son doğrulanmış checkpoint'ten devam et, sıradaki task ID'yi bitir; yeni faz başlatma. Önce git status/HEAD ve evidence doğrula.

Faz Ready for review olunca PROGRESS/evidence/commit ve gerçek cihaz sonucunu incele. Kullanıcı açıkça 'PHASE-XX'i kabul ediyorum; PHASE-YY dosyasını çalıştır' demeden ilerleme yok. Mandatory fail/blocked onayla geçilemez. Aynı oturumun limiti dolarsa checkpoint/handoff; reset yeni faz demek değil. Tek oturum başına tüm docs yükleme; relevant context only. [MASTER_PLAN](MASTER_PLAN.md), [PROGRESS](PROGRESS.md), [SCOPE_TRACEABILITY](SCOPE_TRACEABILITY.md). İlk gerçek veri ancak 06 recovery testleri sonrası. Android/iOS/SMS/cloud lane ayrı. Uygulama build/test henüz yok.
