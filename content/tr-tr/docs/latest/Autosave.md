---
title: Otomatik Kaydetme
menu:
  docs:
    parent: miscellaneous
weight: 7100
aliases:
  - /docs/latest/Autosave/
---

Aegisub, varsayılan olarak açtığınız her altyazı dosyasının bir yedek kopyasını ve (son bir dakika içinde herhangi bir değişiklik yapıldıysa) her dakika bir başka kopyasını otomatik olarak kaydeder. Bu kopyalar Windows'ta `%APPDATA%\Aegisub\autosave`, Linux'ta `~/.aegisub/autosave` ve OS X'te `~/Library/Application Support/Aegisub/autosave` dizinlerinde bulunabilir.
Buna ek olarak, dosyalar doğrudan Aegisub içinde Dosya → Otomatik Kaydedilen Dosyayı Aç... menüsünden görüntülenebilir.

![otomatik-kaydetme-menüsü](/img/3.2/autosave-menu.png#center)

![otomatik-kaydetme-diyaloğu](/img/3.2/autosave-dialog.png#center)

Aegisub, otomatik kaydetme dizinindeki eski dosyaları otomatik olarak temizler, bu nedenle otomatik yedekler dosyaların uzun süreli depolanması için kullanılmamalıdır.