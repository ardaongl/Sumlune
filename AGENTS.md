# Sumlune — Agent çalışma sözleşmesi

## Önce oku
1. README.md, docs/execution/CURRENT_STATE.md, docs/execution/DECISION_REGISTER.md.
2. Göreve göre docs/INDEX.md üzerinden ilgili PRD, mimari, ADR ve kabul kriterleri. Tüm dokümanları her görevde yükleme.
3. Git durumunu ve son handoff'u kontrol et. Kullanıcının değişikliklerini ezme.

## Yetki
- PLANLAMA: Açık onay olmadan uygulama kodu, scaffold, paket kurulumu, build, deployment başlatma.
- Accepted bağlayıcı; Accepted (koşullu) tercih onaylı ancak teknik doğrulama geçmeden üretim bağımlılığı olarak kesinleşmez; Proposed öneri; Pending çözülmemiş; Superseded eski karar. Çelişkiyi görünür kıl, en yeni onaylı ADR'yi esas al.
- Framework, veri modeli, finansal semantik, güvenlik, kapsam ve paket seçimini sessizce değiştirme; ADR ve onay iste.
- İngilizce kod/teknik tanımlayıcı, Türkçe doküman. Küçük, okunabilir feature modülleri; boş katman yok.

## Uygulama aşamasındaki sınırlar
- ADR-0006: lightweight double-entry ve finansal invariants bağlayıcı. Bütçe için en küçük doğru çözümü seç; muhasebe UI, event sourcing/CQRS, ayrı finans backend'i veya gereksiz abstraction ekleme. Onaylı kapsam, veri güvenliği ve testler maliyet adına kaldırılmaz.
- ADR-0002: feature-first modular monolith, pragmatic Clean Architecture, ports & adapters, pnpm ve üç ortak paket bağlayıcı. ADR-0009 uyumluluk kapısını geçmeden paket sürümü kesinleştirme; başarısızlıkta ADR ile onay iste.
- Saf finansal domain RN, Expo, SQLite, Zustand, native SDK'dan bağımsız. SQLite tek finansal veri kaynağı hedefi. Yazımlar application use case üzerinden atomik ve idempotent; widget/analitik doğrudan yazamaz.
- ADR-0010: SQLite INTEGER minor units, JS güvenli integer sınırı (girdi/çıktı/toplam), gerektiğinde BigInt, Decimal.js kur hesabı; küsuratlı binary float para hesabı yok. ISO 4217, tarihsel kur korunur, manuel fallback; ücretli kur API/backend yok. ADR-0011: currency başına FX clearing, HALF_UP, canonical integer-string wire, immutable rate snapshot, reversal/replacement, tek SQLite ve artımlı migration. ADR-0012: ortak ödeme/recurrence, 90 günlük horizon, partial allocation ve actual payment capacity, taksit principal/interest, kart statement remainder ve borç/alacak semantiği bağlayıcı. ADR-0013: yerel deterministik bütçe/birikim/safe-to-spend/forecast/analiz, tek operating cash classifier ve projection, eksik kur/tutar incomplete, ücretli AI/backend yok. ADR-0014: Akbank/Ziraat öncelikli, notification-first, encrypted structured queue ve foreground drain, SMS gated/review-only, explicit trusted push gider auto; banka desteği fixture/cihaz kanıtı olmadan ilan edilmez. ADR-0015: altı widget, tek snapshot v1, default masked, explicit opt-in, no DB/key/direct write, auth deep link; renderer doğrulama şartlı. ADR-0016: local encrypted DB ve ayrı UI auth, portable encrypted backup/crash-safe restore, açık export, aşamalı optional cloud ve CAS conflict review; crypto/provider doğrulama şartlı, lock açıkken widget masked. ADR-0017: Pure Apple tokenlar, 4 içerik tabı + Ekle sheet, 25 UX ailesi, ortak UI ve privacy/accessibility, feature-specific editor; UI cihaz doğrulaması pending. PLAN-09A kalite gate taslağı onaylanmadan nihai blueprint üretme. Transfer ve kart borç ödemesi gider değil, plan gerçekleşmiş gider değil.
- OTP, tam kart numarası, ham banka mesajı, anahtar, gerçek finansal kayıt ve hassas log repo/telemetri/buluta gitmez. Sentetik/maskeli fixture.
- Pure Apple ortak tokenları, erişilebilirlik; iOS sistem fontu Android'e kopyalanmaz.
- Gerçek veriyi silen reset/migration veya history rewrite izinsiz yapılmaz.

## Faz bazlı geliştirme (geliştirme izninden sonra)
- [Codex yürütme protokolü](docs/execution/CODEX_EXECUTION_PROTOCOL.md) uyarınca ayrı Markdown faz blueprint'lerini ve ilerleme kontrolünü kullan. Nihai blueprint'ler PLAN-09'da yazılacak; onlardan önce kodlama yok.
- Kullanıcı tarafından verilen aktif fazın kapsamını aşma; doğrulanmamış işi tamamlandı olarak işaretleme, fazlar arası sapma veya engeli kaydet.

## Görev sonu
Kapsamı küçük tut. İlgili testleri çalıştır, çalıştırılmayanları açıkça belirt. CURRENT_STATE, BACKLOG, SESSION_HANDOFF, gerekiyorsa ADR güncelle. Conventional Commits; kullanıcı yetkisi doğrultusunda commit/push. Doğrulama olmadan tamamlandı deme. Bkz. [Done](docs/engineering/DEFINITION_OF_DONE.md).
