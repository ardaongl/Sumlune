# Codex yürütme protokolü

**Durum:** Gereksinim Accepted; uygulama ayrıntıları Proposed.  
**Tarih:** 2026-11-26.

## Ürün sahibinin gereksinimi
Bütün teknik kararlar tamamlandıktan sonra her geliştirme fazı için ayrı, ayrıntılı Markdown goal prompt/blueprint hazırlanır. Ürün sahibi dosyaları faz faz Codex'e verir. İlerleme kontrol sistemi fazlar arasında sapmayı önler. Şu an planlama sürüyor; nihai blueprint ve kodlama başlamadı.

## Önerilen düzen (PLAN-09'da kesinleşecek)
- `docs/execution/phases/PHASE-00-*.md`, `PHASE-01-*.md` vb.: tek fazın giriş noktası.
- `docs/execution/PROGRESS.md`: tek aktif faz, görev ID ve durum, bağımlılık, doğrulama kanıtı, commit SHA, engeller, sıradaki adım.
- Mevcut CURRENT_STATE, BACKLOG, SESSION_HANDOFF ve DECISION_REGISTER kaynaklarıyla tutarlılık; aynı bilgiyi birden fazla yerde bağımsız güncelleme yok.

## Blueprint içeriği (öneri)
Amaç, neden, önkoşullar, gerekli repo/ADR bağlamı, kapsam ve kapsam dışı, değiştirilecek modüller, sıralı görevler ve ID'ler, kabul kriterleri, test/build komutları, olumsuz senaryolar, güvenlik/finansal invariants, beklenen çıktı, checkpoint, commit ve handoff. Yerel/ücretsiz araçları önceliklendir. Bağlayıcı kararı sessizce değiştirme.

## Faz kapısı (öneri)
Not started → In progress → Blocked / Ready for review → Accepted (Done). Aktif faz sınırı korunur. Test/build sonucu, çalıştırılmayan kontroller ve cihaz doğrulaması açıkça yazılır. Başarısız veya doğrulanmamış zorunlu kontrol geçilmiş sayılmaz. Codex sonraki faza kendiliğinden başlamaz; kullanıcı inceleme ve onayı sonrası yeni blueprint verilir. Her faz kendi çalışır checkpoint'ine ulaşmayı hedefler; riskli iş küçük teknik spike ile erken doğrulanır. Faz sayısı dört reset ile birebir aynı olmak zorunda değil; reset kapasitesi ölçülmedi. Ek harcama ve kapsam değişikliği kullanıcıya sunulur.

## Sonraki iş
PLAN-02 para/kur modeli, PLAN-03 şema, PLAN-04 ödeme ve tahmin, PLAN-05/06/07/08 capture/widget/security/ekran. PLAN-09'da bu protokol kesinleştirilir, nihai faz dosyaları ve progress tracker oluşturulur. DEV-00 ancak açık kodlama izniyle başlar.
