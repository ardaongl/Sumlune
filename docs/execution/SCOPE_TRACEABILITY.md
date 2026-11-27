# Scope Traceability — ADR-0019
35 feature + 4 input methods + 3 cross-cutting delivery commitments; source SCOPE.md, ADR-0003/0005/0016. Mapping is plan, not implementation evidence. All Q evidence in PROGRESS. PHASE-09 audits F01..35/I01..03 local target; I04 permission gate 10, X02/03 optional cloud. iOS capture not supported. UX family details SCREENS/SCREEN_DETAILS. Ranges denote all IDs in range; Q grouped subchecks independently evidenced.
| ID | Requirement | Phase | UX | Q groups |
|---|---|---|---|---|
| F01 | Nakit, banka, kredi kartı | 03 | UX-04/05 | Q-FIN-02 |
| F02 | Hesap transferi | 03 | UX-07/08 | Q-FIN-02/05 |
| F03 | Çoklu para birimi | 02/03 | UX-05/07/21 | Q-FIN-01/05 |
| F04 | Gelir/gider | 03 | UX-06..08 | Q-FIN-02..04 |
| F05 | Özelleştirilebilir kategoriler | 03 | UX-09 | Q-UX-01/02 |
| F06 | Arama/filtre/etiket | 03 | UX-06/09 | Q-UX-02 |
| F07 | Abonelik | 04 | UX-11 | Q-PAY-01/02 |
| F08 | Fatura/kira | 04 | UX-11 | Q-PAY-01/02 |
| F09 | Taksit | 04 | UX-12 | Q-PAY-03 |
| F10 | Tekrarlayan ödeme | 04 | UX-11 | Q-PAY-01 |
| F11 | Borç/alacak | 04 | UX-13 | Q-PAY-04 |
| F12 | Ödeme hatırlatma | 04 | UX-23 | Q-PAY-05 |
| F13 | Finansal takvim | 04 | UX-10 | Q-PAY-01/02 |
| F14 | Gecikmiş ödeme | 04 | UX-14 | Q-PAY-02 |
| F15 | Abonelik yıllık maliyeti | 05 | UX-11/15 | Q-INT-05 |
| F16 | Aylık bütçe | 05 | UX-16 | Q-INT-01 |
| F17 | Kategori bütçesi | 05 | UX-16 | Q-INT-01 |
| F18 | Birikim | 05 | UX-17 | Q-INT-02 |
| F19 | Safe-to-spend | 05 | UX-18/03 | Q-INT-03 |
| F20 | 30/60/90 forecast | 05 | UX-18 | Q-INT-04 |
| F21 | Heatmap | 05 | UX-15 | Q-INT-05 |
| F22 | Hafta/ay/yıl analiz | 05 | UX-15 | Q-INT-05 |
| F23 | Dönem karşılaştırma | 05 | UX-15 | Q-INT-05 |
| F24 | Widget Günlük harcama | 08 | UX-22 | Q-WID-01..03 |
| F25 | Widget Yaklaşan ödeme | 08 | UX-22 | Q-WID-01..03 |
| F26 | Widget Abonelik | 08 | UX-22 | Q-WID-01..03 |
| F27 | Widget Aylık bütçe | 08 | UX-22 | Q-WID-01..03 |
| F28 | Widget Hızlı harcama | 08 | UX-22 | Q-WID-01..03 |
| F29 | Widget Hesap bakiyesi | 08 | UX-22 | Q-WID-01..03 |
| F30 | Biometrik lock | 01/06 | UX-02/23 | Q-SEC-02 |
| F31 | Offline kullanım | 01..09 | UX-01..24 | Q-UX-01/05 Q-REL-02 |
| F32 | Backup/restore | 06 | UX-24 | Q-SEC-03/04 |
| F33 | CSV/JSON export | 06 | UX-24 | Q-SEC-05 |
| F34 | Hassas tutar gizleme | 01/03/05/08 | UX-03/21/22 | Q-UX-05 Q-WID-01 |
| F35 | TR/EN | 01..09 | UX-01..24 | Q-UX-04 |
| I01 | Manuel giriş | 03 | UX-07 | Q-UX-01 |
| I02 | Hızlı şablon | 03 | UX-07/09 | Q-UX-01 |
| I03 | Android banka push | 07 | UX-19/20 | Q-CAP-01..05 |
| I04 | Android SMS izinli | 10 | UX-19/20 | Q-CAP-01..05 SMS |
| X01 | Hibrit trusted automation | 07 | UX-19/20 | Q-CAP-02/03 |
| X02 | Optional encrypted cloud backup | 11 | UX-25 | Q-CLOUD-01 |
| X03 | Optional multi-device CAS sync | 12 | UX-25 | Q-CLOUD-02 |
