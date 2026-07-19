---
title: utils.lua
menu:
  docs:
    parent: lua-modules
weight: 6262
aliases:
  - /docs/latest/Automation/Lua/Modules/util/
---

Automation 4 Lua dahil etme dosyası `utils.lua`, Lua betikleri yazmaya yardımcı olacak çeşitli destek işlevlerini içerir.
Dosya için genel bir konu yoktur.

## Kullanım

Bu modülü {{< lua `util = require 'aegisub.util'` >}} ile içe aktarın

## Tablo işlevleri

Tabloları çeşitli yollarla kopyalamak yaygın bir görevdir.
`util`, en yaygın durumları ele almak için bazı işlevler sağlar.

### copy

Özet: {{< lua `newtable = util.copy(oldtable)` >}}

Parametre olarak iletilen tablonun yüzeysel bir kopyasını oluşturur.
Buradaki yüzeysel ifadesi, içerilen tabloların içine dalmadığı ve onları da kopyalamadığı anlamına gelir.
Örneğin, `oldtable.st` bir tabloya referans veriyorsa, `newtable.st` aynı tabloya referans verecektir ve `newtable.st` üzerinde yapılan değişiklikler `oldtable.st` üzerinde de yansıtılacak ve tersi de geçerli olacaktır.

### deep_copy

Özet: {{< lua `newtable = util.deep_copy(oldtable)` >}}

Parametre olarak iletilen tablonun derin bir kopyasını oluşturur.
Bu işlev, dairesel referansları ele almaya ve üzerlerinde sonsuz özyineleme yapmamaya çalışsa da, her durumda çalışmayabilir.
Bu işlevi nadiren kullanmanız gerekecektir.
Derin bir kopya almanız gerektiğini düşünüyorsanız, görevinizi bir kez daha gözden geçirin.

## Renk işlevleri

Renk verileri üzerinde çeşitli dönüşümler yapmak genellikle yararlıdır. Bunun için birkaç işlev dahil edilmiştir.

### ass_color

Özet: {{< lua `colorstring = util.ass_color(r, g, b)` >}}

Verilen `r`, `g` ve `b` bağımsız değişkenlerinden `&HBBGGRR` biçiminde bir ASS renk dizesi oluşturur.

Uyarı: Bağımsız değişkenlerin aralık kontrolü yapılmaz.
0..255 aralığının dışındaki değerler hatalı çıktı üretecektir.

### ass_alpha

Özet: {{< lua `alphastring = util.ass_alpha(a)` >}}

Verilen `a` bağımsız değişkeninden `&HAA&` biçiminde bir ASS alfa dizesi oluşturur.

Giriş aralığını kontrol etmez.

### ass_style_color

Özet: {{< lua `colorstring = util.ass_style_color(r, g, b, a)` >}}

Stil tanımlarında kullanım için uygun bir ASS renk dizesi, yani `&HAABBGGRR` biçiminde oluşturur.

Giriş aralığını kontrol etmez.

### extract_color

Özet: {{< lua `r, g, b, a = util.extract_color(colorstring)` >}}

Bir renk dizesinden renk bileşenlerini çıkarır. Birkaç renk dizesi formatı tanınır:

- Stil tanımı: `&HAABBGGRR`
- Satır içi geçersiz kılma (override): `&HBBGGRR&`
- Alfa geçersiz kılma: `&HAA&`
- Alfa ile HTML: `#RRGGBBAA`

Bu işlevin geçerli bir renk dizesi iletildiğinde her zaman dört sayı döndürdüğünü unutmayın.
Kullanılmayan değerler (renk dizesinin biçimine bağlıdır) 0 (sıfır) olarak atanır.
Tanınmayan bir renk dizesi iletilirse, `nil` döndürülür.

{{<example-box>}}

```lua
r, g, b, a = extract_color("&H7F&")
```

`r`, `g` ve `b` 0 olacaktır; `a` 127 olacaktır.
{{</example-box>}}

### alpha_from_style

Özet: {{< lua `alphastring = util.alpha_from_style(coloralphastring)` >}}

Bir renk dizesinin alfa kısmını, alfa geçersiz kılma dizesi olarak, yani `&HAA&` biçiminde döndürür.
Bu işlev, `extract_color` ve `ass_alpha` bileşenlerinden oluşur.

### color_from_style

Özet: {{< lua `colorstring = util.color_from_style(coloralphastring)` >}}

Bir renk dizesinin renk kısmını, renk geçersiz kılma dizesi olarak, yani `&HBBGGRR&` biçiminde döndürür.
Bu işlev, `extract_color` ve `ass_color` bileşenlerinden oluşur.

### HSV_to_RGB

Özet: {{< lua `r, g, b = util.HSV_to_RGB(h, s, v)` >}}

Ton, Doygunluk, Değer uzayında verilen bir rengi Kırmızı, Yeşil, Mavi uzayına dönüştürür.

`h` derece cinsinden verilir.
Nominal aralık 0..359'dur; bu aralığın dışındaki değerler buna çevrilecektir.
`s` ve `v` giriş aralığı 0..1'dir.
Bunlar aralık kontrolünden geçirilmez.
`r`, `g` ve `b` çıkış aralığı 0..255'tir.

## Dize işlevleri

Lua standart `string` kütüphanesi oldukça sınırlı olduğundan, birkaç ek yardımcı işlev sağlanmıştır.
Ayrıca bkz. [unicode]({{< relref "unicode" >}}).

### string.trim

Özet: {{< lua `outstring = util.trim(instring)` >}}

Giriş dizesinin başındaki ve sonundaki tüm boşluk karakterlerini kaldırır ve dönüştürülmüş dizeyi döndürür.

Uyarı: Bu işlev UTF-8 güvenli değildir.
Boşlukları eşleştirmek için Lua regex `%s` sınıfını kullanır, bu da bazı eski kodlamalarda UTF-8 kodlu metindeki bazı önek baytlarıyla da eşleşmesine neden olacaktır.

### string.headtail

Özet: {{< lua `head, tail = util.headtail(instring)` >}}

Bir dizeyi, birkaç işlevsel dildeki bağlantılı liste işlemeye benzer şekilde, ilk boşluk dizisine göre bir "baş" (head) ve bir "kuyruk" (tail) olarak böler.

`instring` herhangi bir boşluk karakteri içermiyorsa, `instring, ""` döndürür.

### string.words

Özet: {{< lua `for word in util.words(instring) do ... end` >}}

`string.headtail` semantiklerini kullanarak dizedeki tüm kelimeler üzerinde döngü kurmak için bir `for` döngüsünde kullanılmak üzere bir yineleyici işlev döndürür.

## Sayısal işlevler

Sayılar üzerinde çeşitli işlemleri gerçekleştiren işlevler.

### clamp

Özet: {{< lua `outval = util.clamp(inval, min, max)` >}}

`inval` değerini `min`..`max` aralığında olacak şekilde sınırlar (clamp).

### interpolate

Özet: {{< lua `outval = util.interpolate(t, a, b)` >}}

`a` ve `b` arasında enterpolasyon yapar.
`t` 0..1 aralığındaki zaman değişkenidir.
Bu aralığın dışındaki değerler sınırlandırılır.

### interpolate_color

Özet: {{< lua `outcolor = util.interpolate_color(t, color1, color2)` >}}

`t` zaman değişkeni 0..1 aralığında olmak üzere `color1` ve `color2` arasında enterpolasyon yapar.
`color1`, `color2` ve `outcolor` renk dizeleridir ve `outcolour` renk geçersiz kılma biçiminde olacaktır.

### interpolate_alpha

Özet: {{< lua `outalpha = util.interpolate_alpha(t, alpha1, alpha2)` >}}

`interpolate_color` ile benzerdir, ancak bunun yerine alfa değerlerini enterpole eder.
Ayrıca renk dizeleri üzerinde çalışır ve bir alfa geçersiz kılma dizesi döndürür.