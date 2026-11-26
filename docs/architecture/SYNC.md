# Local-first ve opsiyonel bulut

Accepted: internet ve üyelik olmadan temel kullanım; opsiyonel bulut backup ve cihazlar arası sync. Proposed: şifreli yerel DB/yedek ilk sürüm; canlı bulut daha sonra, Supabase aday, vendor bağımsız portlar.

SQLite birincil kaynak. Ağ arızası temel işlemi durdurmaz. Bulut kapanınca yerel kayıt kalır. Telefon değişimi, Android→iOS ve restore hedefi.

Aday protokol: transaction ile outbox, revision/device ID, retry/backoff, idempotency, tombstone, pull cursor; journal/postings atomik aggregate. Sessiz last-write-wins yok; conflict çözümü tasarlanır. Ham banka mesajı sync dışı. E2EE cihaz eşleme/key recovery/protokol/metadata leakage/hesap silme pending. Şifreli backup ve çok cihazlı sync ayrı teslimat; bulut kapsamdan çıkarılmadı.
