---
title: Lua Modülleri
menu:
  docs:
    parent: lua-reference
    identifier: lua-modules
weight: 6260
aliases:
  - /docs/latest/Automation/Lua/Modules/
---

Aegisub ile birlikte bir dizi Lua modülü gelmektedir.
Bunlardan [`karaskel.lua`]({{< relref "karaskel.lua.md" >}}) gibi bazıları altyazıya özel işlevleri yerine getirirken, [re]({{< relref "re" >}}) gibi diğerleri Lua standart kütüphanesindeki eksiklikleri giderir.

## Modüllerin kullanımı

Betiğin en üst kısmına `modulename = require 'aegisub.modulename'` yazmanız yeterlidir.
Örneğin, [re]({{< relref "re" >}}) modüllerini dahil etmek için `re = require 'aegisub.re'` kullanın.

Eski betiklere bakarsanız, `include` gibi modülleri dahil etmek için kullanılan birkaç başka yöntem görebileceğinizi unutmayın.
Bunlar, Lua 5.2 ile tanıtılan modern Lua modül stiline geçilmesiyle kullanımdan kaldırılmıştır.

[Karaoke Templater]({{< relref "../Karaoke_Templater" >}}) içinde modülleri kullanmak için, `require` ifadesini bir [code once]({{< relref "../Karaoke_Templater/Code_lines_and_blocks#classes-of-code-lines" >}}) satırına yerleştirin.
`karaskel.lua`, `utils.lua` ve `unicode.lua` dosyalarının [Karaoke Templater]({{< relref "../Karaoke_Templater" >}}) içinde `require` edilmesine gerek yoktur, çünkü bunlar otomatik olarak içe aktarılır.

## Modül referansı

[util]({{< relref "Modules/util" >}})
: Özellikle renkleri işlemek için kullanılan ve belirli bir kategoriye tam olarak uymayan çeşitli yardımcı işlevlerden oluşan bir koleksiyon.

[`karaskel.lua`]({{< relref "Modules/karaskel.lua.md" >}})
: Karaoke iskeleti, temel olarak gelişmiş karaoke efektleri oluşturmak amacıyla zamanlanmış karaokelerin metin düzenini yapmak için tasarlanmış bir işlev koleksiyonu ve bir dizi diğer yardımcı işlevdir.

[unicode]({{< relref "Modules/unicode" >}})
: Aegisub'a Otomasyon 4 Lua arayüzü aracılığıyla girip çıkan tüm veriler UTF-8 olarak kodlanmıştır, ancak Lua bunu yerel olarak desteklemez.
  Burada çeşitli yardımcı işlevler sunulmaktadır.

[`cleantags.lua`]({{< relref "Modules/cleantags" >}})
: Bir satırdaki ASS etiketlerini temizlemek için kullanılan bir işlev.

[clipboard]({{< relref "Modules/clipboard" >}})
: Metin kopyalama ve yapıştırma işlevleri.

[re]({{< relref "Modules/re" >}})
: Tam Unicode desteğine sahip olan ve Lua'nın yerleşik düzenli ifadelerinden daha fazla özellik sunan, [boost.regex](https://www.boost.org/doc/libs/1_53_0/libs/regex/doc/html/index.html) aracılığıyla sağlanan ICU düzenli ifade bağlayıcıları.

[lpeg](https://www.inf.puc-rio.br/~roberto/lpeg/)
: Ayrıştırıcılar yazmak için PEG kütüphanesi.

[luabins](https://github.com/agladysh/luabins)
: Tabloları ek verilere veya yapılandırma dosyalarına kaydetmek için bir serileştirme kütüphanesi.

[lfs](https://lunarmodules.github.io/luafilesystem/)
: Lua standart kütüphanesi tarafından desteklenmeyen çeşitli dosya sistemi işlevleri.