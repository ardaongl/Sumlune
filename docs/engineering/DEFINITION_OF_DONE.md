# Definition of Done — Accepted (ADR-0018)

Planlama: karar statüsü açık, ADR/bağımlı doküman tutarlı, risk ve sonraki adım kayıtlı, onay gereken yer işaretli.

Kod (ancak izin sonrası): kabul kriterleri, domain sınırları, ilgili test/format/lint/typecheck ve mümkünse cihaz/build doğrulaması; çalıştırılmayan kontrol açıkça kayıtlı; docs/handoff güncel; secrets/gerçek veri yok; küçük incelenebilir commit. Başarısız build/test ile görev tamamlanmış sayılmaz. Mock başarı gerçek cihaz başarısı değildir.

## PLAN-09A bağlayıcı kalite kapısı
Task tamamlanması: kapsam/kabul kriterleri ve bağlı QUALITY_MATRIX ID'leri geçer, ilgili tests/typecheck/lint/format, actual commit/evidence, hiçbir P0/P1 ilgili açık hata yok. Faz tamamlanması: tüm mandatory task ve faz gate kanıtlı, run edilmeyenler gerekçeli; zorunlu kontrol geçmeden Ready for review yok. Blocked gerçek durum, ilerleme yüzdesi başarı kanıtı değil. Kullanıcı review/accept olmadan sonraki faz başlatılmaz. Release için TEST_STRATEGY release gates. Git SHA, command/exit/count/coverage/device ve sanitize evidence. Docs-only plan onayı implementation/test başarısı değildir. Bu ayrıntılar Accepted. Phase gate ve Q alt kontrol kapsamı blueprint/progress'te. Test edilen commit ve evidence-only commit ayrılır; code değişirse ilgili kanıt yeniden çalıştırılır. Kullanıcı faz kabulü mandatory başarısızlığı geçersiz kılamaz; blocked kalır. P2 sapması açıklanarak review edilir.
