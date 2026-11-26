# ADR-0006 — Lightweight double-entry finansal motor

**Durum:** Accepted  
**Tarih:** 2026-11-26  
**Karar yetkisi:** Ürün sahibi bütçe ve geliştirme yükünü gözeterek kayıt modeli seçimini asistana devretti.

## Bağlam
Kısıtlı Codex limitleri ve düşük işletim maliyeti; kredi kartı, transfer, borç/alacak, iade, taksit, çoklu para birimi ve planlama kapsamı korunacak. Amaç kişisel finans takibi, profesyonel muhasebe yazılımı değil.

## Karar
Lightweight double-entry: accounts, journal_entries ve postings kavramsal çekirdeği, saf TypeScript motor. Varlık, yükümlülük, gelir, gider ve açılış/düzeltme için gereken dengeleme hesabı; teknik hesaplar kullanıcıdan gizli. Normal işlem en az iki posting; yalnız gerçekten gerekli durumlarda daha fazla. Ortak küçük posting builder/validator ve bir atomik repository yazımı; ayrı kurumsal muhasebe altyapısı yok.

Bağlayıcı invariants: dengeli kayıt (aynı para birimi veya henüz tasarlanacak açık FX değerleme kuralları); atomik yazım; idempotent kaynak/komut; kesin para aritmetiği; izlenebilir düzeltme/iptal; bakiye posting'lerden türetilir; ödeme planı gerçekleşmiş işlem değildir; belirli girdilerle deterministik domain; UI/DB/native bağımsızlığı. Kart alışverişi gider, kart borcu ödeme transfer; nakit/banka transferi gider veya gelir değil. Açılış bakiyesi düzeltme kaydıyla; iade orijinal işlemle ilişkilendirilir.

## Alternatifler
Single-entry daha kısa başlangıç ancak transfer/kart/iade/borç özel kuralları çoğalır. Tam kapsamlı double-entry/ERP gereksiz kapsam ve bakım yükü. Seçilen küçük model ortak invariants sağlar; doğruluğu testlerle kanıtlanır. Maliyet avantajı tahmindir, ölçülmedi.

## Bilinçli sınırlar
- Muhasebe arayüzü, kullanıcı yönetimli hesap planı, resmi raporlar, vergi, dönem kapatma, event sourcing/CQRS, ayrı finans backend'i yok.
- SQLite ve mevcut paket sınırları; ek servis/paket sadece zorunlu gerekçe ile. Yerel motor ücretli API gerektirmez.
- Basit revizyon/iptal izi, atomik repository ve testler yeterli hedef; event store veya genel kural motoru yok. Kesin edit/reversal şeması PLAN-03'te.
- Onaylı ürün kapsamı çıkarılmadı. Para temsili, FX/yuvarlama, recurrence, taksit ve kesin SQL şeması ayrı karar; teknik uygulama ve performans doğrulanmadı.
