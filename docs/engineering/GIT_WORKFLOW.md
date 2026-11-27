# Git çalışma akışı

Hedef private ardaongl/Sumlune, main, Türkçe doküman, İngilizce kod, Conventional Commits (ADR-0019 yürütme standardı). Başlangıç yalnız Markdown. Karar: tartış → açık onay → ADR + ilgili doküman + karar kaydı → doğrula → commit. Kodlama için ayrı onay. Küçük değişiklik seti; gerektiğinde feature branch ve PR. Branch protection/CI henüz kurulmadı. Force push/destructive işlem izinsiz yok. Gerçek finansal veri, secrets veya yedek commit edilmez. Gerçek commit SHA Git geçmişinde doğrulanır.

Phase code checkpoint ve evidence-only commit ayrı; gerçek tested SHA PROGRESS'e yazılır. User phase acceptance ayrı kaydedilir; push yalnız yetkiyle. No force/reset. Local değişiklikleri koru.
