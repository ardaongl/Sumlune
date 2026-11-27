# Pure Apple tasarım sistemi

Görsel yön **Accepted**: Apple Wallet finansal sadelik, Health veri hiyerarşisi, Calendar planlama, Settings grouped list. Android/iOS ortak kimlik; UIKit Android'e taşınmaz. Kopyalama değil HIG referansı. No AI look, gereksiz gradient/gölge/dekoratif kart yok; işlevsel renk, güçlü tipografi, native hissi, haptic feedback ve erişilebilirlik.

Light/dark/system. iOS SF Pro sistem fontu, Android Inter (tercih; lisans ve font scaling doğrulanır, sistem fallback); SF Pro dosyası Android'e paketlenmez. Tabular numerals, dinamik font, ekran okuyucu, kontrast, reduce motion, safe area, 48dp touch hedefi. Native sistem dialog ve izin OS'e uygun. Cam efektleri yalnız navigasyon/overlay, okunabilirlik uygunsa; zorunlu değil. Ortak StyleSheet ve token, keyfi hardcoded stil yok. Development-only küçük UI Playground, ayrı servis yok.

Referans: https://developer.apple.com/design/human-interface-guidelines/ ve https://developer.apple.com/design/resources/ . Tokenlar/ekranlar ADR-0017 Accepted; gerçek cihaz doğrulaması yok.

ADR-0017: 4 içerik tabı + Ekle aksiyonu, grouped lists, reusable editor/detail/sheet, görsel hiyerarşide finansal tutar ve next action. [SCREENS](SCREENS.md) ve [SCREEN_DETAILS](SCREEN_DETAILS.md). Tasarım tokenları ve ekran sözleşmesi onaylandı; Figma veya gerçek cihaz çıktısı yok.

Cam efekti ilk sürümde zorunlu değil; düz/opaque surface varsayılan. Sistem klavyesi ve OS dialog, ortak StyleSheet/theme hook, platform-native davranış; gereksiz UI framework ve animasyon paketi yok. Visual regression ilk etap manuel screenshot + kritik UI assertions.
