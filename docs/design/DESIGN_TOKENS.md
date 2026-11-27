# Tasarım tokenları — Accepted (ADR-0017)

| Token | Light | Dark |
|---|---|---|
| Background | #F2F2F7 | #000000 |
| Surface | #FFFFFF | #1C1C1E |
| Elevated surface | #FFFFFF | #2C2C2E |
| Primary text | #000000 | #FFFFFF |
| Secondary text | #636366 | #AEAEB2 |
| Separator | #D1D1D6 | #38383A |
| Accent | #007AFF | #0A84FF |
| Income | #248A3D | #30D158 |
| Expense | #D70015 | #FF453A |
| Warning | #A65E00 | #FF9F0A |

Kategori ikon varsayılanları: market #34C759, yemek #FF9500, ulaşım #007AFF, ev #5856D6, alışveriş #FF2D55, abonelik #AF52DE, sağlık #FF3B30, eğitim #5AC8FA, eğlence #FF9500, seyahat #5856D6, gelir #30B060, diğer #8E8E93. Renk tek anlam taşıyıcısı olmaz; kullanıcı ikon/rengi seçebilir.

| Typography | Size | Weight |
|---|---|---|
| Financial Display | 40 | semibold |
| Large Title | 34 | bold |
| Title 1 | 28 | semibold |
| Title 2 | 22 | semibold |
| Headline | 17 | semibold |
| Body | 17 | regular |
| Subheadline | 15 | regular |
| Footnote | 13 | regular |
| Caption | 11 | regular |

RN logical dp/point; font scaling korunur. Spacing 4/8/12/16/20/24/32/40; ekran kenarı 20; row min 52; touch min 48; radius 8/12/16/24; ikon 16/24; separator hairline; motion 150–350ms; default shadow yok. Kontrast doğrulanacak; mavi küçük metinde yüzeye göre uyarlanır.

## Uygulama politikası
Brand accent yukarıdaki değerleri korur; küçük link metni/filled CTA için semantic accessible contrast variant gerekir. Light accentText/primaryAction aday #005FCC (white/on-light), dark accentText #64B5FF, filled action foreground black on bright dark accent; her pairing WCAG AA 4.5:1 normal, 3:1 büyük/meaningful controls ölçümle doğrulanır. Test başarısızsa semantic variant düzelt, brand palette sessizce değiştirme. Category renkleri ikon/arka plan; metin semantic primary. Color-only error/status yok. Font dynamic scaling (200% test), wrap ve row min değil fixed height; money display gerekirse wrap/accessible alternative, ellipsis ile tutar kaybetme yok. Spacing ve radii ortak token; haptic/motion reduce-motion'a saygılı, motion gereksizse yok. Inter lisansı ve native font fallback gate; iOS system font dağıtılmaz.
