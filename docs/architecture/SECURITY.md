# Güvenlik — kapsam Accepted, teknik Proposed

Tehdit: cihaz kaybı, widget/lockscreen ifşası, izin, hassas log, şifresiz backup, migration, bulut hesap erişimi, sahte banka mesajı. Ele geçirilmiş cihaz için mutlak güvenlik yok.

- Şifreli SQLite (SQLCipher aday), OS güvenli anahtar saklama, biometric UI ve gerekirse PIN/kurtarma. Background worker key erişimi ayrı sorun ve spike.
- Widget minimum snapshot; masked ise açık değer yok. Preview/screenshot politikası platforma uygun değerlendirilecek.
- Şifreli, bütünlük doğrulamalı backup; KDF/anahtar yönetimi pending. Açık CSV/JSON export uyarısı ve güvenli paylaşım.
- Ham SMS, OTP, banka bildirimi, kişisel veri/secrets log/telemetri/bulut/repo yok; maskeli fixture.
- Opt-in izin, allowlist, izin iptali; manuel devam.
- Bulut E2EE hedefi; Supabase tek başına sağlamaz. Silme/export/kurtarma ayrı tasarım.

Kişisel APK/Play SMS izinleri ve iOS signing koşulları doğrulanacak; review ve cihaz testi yok.

ADR-0014: capture queue yalnız structured alan, Keystore-backed AES-GCM, HMAC ayrı key, 7 gün/500 event, pending 30 gün, no raw persist/log/network, review-first restore/rotation. Key lifecycle ve retention güvenlik planında tamamlanır. Widget snapshot privacy varsayılan masked ve explicit opt-in önerisi PLAN-06; launcher cache temizliği OS kontrolünde, kesin anlık gizleme vaat edilmez.
