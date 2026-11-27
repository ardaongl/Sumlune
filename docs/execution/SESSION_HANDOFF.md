# Oturum devri

2026-11-28 — PLAN-02 Money & Currency onayı, PLAN-03 başlangıcı. Önceki commit e3cb84cb04351156943dfae86908cdd606b6eb20. Kodlama yetkisi yok.

ADR-0006 lightweight double-entry, ADR-0002 modular monolith Accepted. ADR-0009 stack koşullu. ADR-0010 Accepted: minor units INTEGER, safe integer, gerektiğinde BigInt/Decimal.js, TRY default, ISO 4217, değiştirilebilir raporlama, tarihsel kur ve hibrit kur. Ücretli kur API/backend yok. Frankfurter aday; dokümanları incelendi, canlı entegrasyon/cihaz testi yok. Kur/para ayrıntıları [MONEY_CURRENCY](../architecture/MONEY_CURRENCY.md).

PLAN-03 şema taslağı [DATABASE](../architecture/DATABASE.md) içinde Proposed. Sonraki oturum Git HEAD, AGENTS, CURRENT_STATE, DECISION_REGISTER, DATABASE, MONEY_CURRENCY ve ADR-0010 oku. Çekirdek tabloları, constraint ve artımlı migration ile FX clearing, rounding/wire ve düzeltme politikalarını görüş/onayla; PLAN-04 sonra. Diğer modül şemaları ilgili aşamada tamamlanır.

Kullanıcı istediği faz başına ayrı Markdown goal prompt/blueprint ve ilerleme kontrolü [CODEX_EXECUTION_PROTOCOL](CODEX_EXECUTION_PROTOCOL.md) içinde; nihai dosyalar PLAN-09. Codex gelecekte Context Recovery → Task Selection → Implementation → Verification → Documentation → Git Checkpoint → Session Handoff. Uygulama kodu, paket kurulumu, build, cihaz testi yok.
