---
title: Otomasyona Genel Bakış
menu:
  docs:
    parent: automation
weight: 6000
aliases:
  - /docs/latest/Automation/
---

**Otomasyon** ismi, Aegisub'ın tüm betik (scripting) işlevselliğini kapsar.

## Otomasyon Hakkında

Otomasyonun tek amacı — isminden de anlaşılacağı üzere — altyazı oluşturma ve düzenlemenin çeşitli yönlerini otomatikleştirmektir.
Bu özellik başlangıçta ağırlıklı olarak [karaoke efektleri]({{< relref "Glossary/Karaoke_effect" >}}) oluşturmak için kullanılıyordu, ancak zamanla kapsamı genişleyerek Aegisub'a gelişigüzel yeni işlevler ekleyen daha genel amaçlı [makroları]({{< relref "Glossary/Macro" >}}) destekleyecek hale geldi.

Otomasyonun hedeflerinden bazıları:

- Karmaşık altyazı düzenleme görevlerini otomatikleştirmek için makrolar
- Daha basit girdilerden karmaşık efektler üretmek için dışa aktarma filtreleri
  - Karaoke efektleri
  - Çeviri notu kutuları
- Muhtemelen henüz keşfedilmemiş birkaç kullanım alanı daha

## Otomasyonu Kullanma

Aegisub, halihazırda paketlenmiş ve kullanıma hazır birkaç Otomasyon betiği ile birlikte gelir.
Buna gelişmiş **[Karaoke_Templater]({{< relref "Karaoke_Templater" >}})** betiği ve bazı düzenleme görevlerini basitleştirmek için bir [makro koleksiyonu]({{< relref "Included_macros" >}}) dahildir.

Aegisub'da neredeyse her zaman aynı anda birkaç Otomasyon betiği yüklüdür.
Hangi betiklerin yüklü olduğunu görebilir ve **[Otomasyon/Yönetici]({{< relref "Automation/Manager" >}})** penceresinden daha fazlasını yükleyebilir/kaldırabilirsiniz.

Tüm Otomasyon betikleri kendilerini Aegisub'da bir şekilde gösterir.
Bazıları [Otomasyon menüsündeki makrolar]({{< relref "Running_macros" >}}) olarak görünürken, diğerleri [Dışa Aktar iletişim kutusundaki filtreler]({{< relref "Exporting" >}}) olarak görünür.
Hatta bazı betikler her iki yerde de görünür.

## Programcılar için Otomasyon

Otomasyon, [Lua 5.2 modunda](https://www.lua.org/manual/5.2/) derlenmiş [LuaJIT 2.0](https://luajit.org/) kullanır.
[MoonScript](https://www.moonscript.org) yerel olarak desteklenir (aslında Aegisub kütüphanelerinin bazı bölümleri bununla yazılmıştır).

Kendi betiklerinizi yazmaya başlamanıza yardımcı olması için Aegisub ile birlikte gelen birkaç örnek betik bulunmaktadır.
Küçük bir uyarı: Deneyimli bir programcı değilseniz, _kara-templater.lua_ betiği başlamak için çok kötü bir yerdir!