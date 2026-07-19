---
title: re
menu:
  docs:
    parent: lua-modules
weight: 6266
aliases:
  - /docs/latest/Automation/Lua/Modules/re/
---

`re` modülü, Lua'nın yerleşik düzenli ifadelerinin (regular expressions) tam bir alternatifi olarak tasarlanmış, boost::regex etrafında bir sarmalayıcıdır (wrapper). Lua'nınkine göre iki ana avantajı vardır:

1. Tam Unicode desteği. Lua düzenli ifadeleri karakterler yerine baytlar üzerinde işlem yapar, bu da çok baytlı karakterlerle sıklıkla sorunlara neden olur.
2. Daha güçlü ve esnek bir sözdizimi. Teknik olarak Lua, düzenli ifadeleri desteklemez; bunun yerine düzenli ifadelerle yapılabileceklerin küçük bir alt kümesini destekleyen temel bir desen eşleştirme dili vardır. Öte yandan boost::regex, Perl ile uyumlu düzenli ifadeleri destekler.

## Kullanım

Bu modülü {{< lua `re = require 'aegisub.re'` >}} ile içe aktarın.

Düzenli ifade sözdizimi hakkında bilgi için [boost.regex dokümantasyonuna](https://www.boost.org/doc/libs/1_53_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) bakın. Genel olarak, web üzerinde Perl düzenli ifadeleri veya PCRE'den bahseden tüm kaynaklar bu modülün düzenli ifadeleri için geçerli olacaktır.

### Eşleşme Tabloları (Match Tables)

Aşağıdaki işlevlerin birçoğu, aşağıdaki alanları içeren tablolar olan Eşleşme Tabloları döndürür:

`str` (`string`)
: Bir desen veya yakalama ifadesi (capturing expression) tarafından eşleştirilen metin.

`first` (`number`)
: `str` ifadesinin, üzerinde düzenli ifade uygulanan orijinal dizedeki başlangıç indeksi. Bu indeksin bire dayalı olduğunu ve Lua'nın dize indekslemesiyle eşleşmesi için karakterler yerine bayt cinsinden olduğunu unutmayın.

`last` (`number`)
: `str` ifadesinin, üzerinde düzenli ifade uygulanan orijinal dizedeki bitiş indeksi. Bu indeksin bire dayalı, kapsayıcı olduğunu ve Lua'nın dize indekslemesiyle eşleşmesi için karakterler yerine bayt cinsinden olduğunu unutmayın.

{{<example-box>}}

```lua
>>> re.match("b", "abc")
{
    {
        ["str"] = "b",
        ["first"] = 2,
        ["last"] = 2
    }
}
```

{{</example-box>}}

### Bayraklar (Flags)

Aşağıdaki bayraklar, tüm statik işlevlere (`re.compile` dahil) aktarılabilir. Bayraklar, sağlanan tüm bayrak dışı bağımsız değişkenlerden sonra gelmelidir, ancak isteğe bağlı bağımsız değişkenler atlanabilir.

re.ICASE
: Eşleştirme yaparken büyük/küçük harfi yoksay.

re.NOSUB:
: Geriye dönük başvuruları (backreferences) ve yakalama gruplarını ayarlama. İhtiyaç duyulmadığında performansı artırabilir.

re.NEWLINE_ALT:
: Yeni satır karakterlerini alternatif operatörü (|) olarak kabul et.

re.NO_MOD_M:
: ^ ve $ sadece yeni satırlardan ziyade dizenin başı ve sonu ile eşleşir.

re.MOD_S:
: Yeni satırları '.' tarafından eşleştirilen normal karakterler olarak kabul et.

re.MOD_X:
: İfadede kaçış karakteri olmayan boşlukları yoksay, bu da *salt yazılır olmayan* düzenli ifadeler yazmayı mümkün kılar.

re.NO_EMPTY_SUBEXPRESSION:
: Boş ifadeleri/alternatifleri eşleştirme.

{{<example-box>}}

```lua
>>> re.match("a", "A")
nil
>>> re.match("a", "A", re.ICASE, re.NOSUB)
{
    {
        ["str"] = "A",
        ["first"] = 1,
        ["last"] = 1
    }
}
```

{{</example-box>}}

### re.compile

Özet: {{< lua `expr = re.compile(pattern, [FLAGS])` >}}

Bir düzenli ifadeyi derler. Derlenmiş bir düzenli ifadeyi yeniden kullanmak, her kullanıldığında yeniden derlemekten daha hızlıdır ve genellikle daha okunabilirdir.

`@pattern` (`string`)
: Derlenecek düzenli ifade.

`expr` (`table`)
: Aşağıda listelenen tüm işlevlere sahip, ancak desen ve bayrak bağımsız değişkenleri olmayan bir tablo.

{{<example-box>}}

```lua
>>> expr = re.compile("a")
>>> expr:split("banana")
{
    "b",
    "n",
    "n"
}
```

{{</example-box>}}

### re.split

Özet: {{< lua `chunks = re.split(str, pattern, skip_empty=false, max_splits=0)` >}}

Dizeyi, `pattern`'in her bir oluşumunda böl.

`@str` (`string`)
: Bölünecek dize.

`@pattern` (`string`)
: Dizenin bölüneceği düzenli ifade. Desendeki yakalama grupları yoksayılır.

`@skip_empty` (`boolean`)
: Sonuçlara sıfır uzunluklu parçaları dahil etme.

`@max_splits` (`number`)
: Sıfırdan büyükse, dizeyi bölmek için maksimum deneme sayısı (örneğin `#chunks` en fazla `max_splits + 1` olacaktır).

`chunks` (`table`)
: `pattern` eşleşmeleri arasında `str`'nin her bir bölümünü içeren bir tablo.

{{<example-box>}}

```lua
>>> re.split(",", "a,,b,c")
{
    "a",
    "",
    "b",
    "c"
}
```

{{</example-box>}}
{{<example-box>}}

```lua
>>> re.split(",", "a,,b,c", true)
{
    "a",
    "b",
    "c"
}
```

{{</example-box>}}
{{<example-box>}}

```lua
>>> re.split(",", "a,,b,c", false, 1)
{
    "a",
    ",b,c",
}
```

{{</example-box>}}

### re.gsplit

Özet: {{< lua `iter = re.gsplit(str, pattern, skip_empty=false, max_splits=0)` >}}

re.split işlevinin yineleyici (iterator) sürümü.

`@str` (`string`)
: Bölünecek dize.

`@pattern` (`string`)
: Dizenin bölüneceği düzenli ifade. Desendeki yakalama grupları yoksayılır.

`@skip_empty` (`boolean`)
: Sonuçlara sıfır uzunluklu parçaları dahil etme.

`@max_splits` (`number`)
: Sıfırdan büyükse, dizeyi bölmek için maksimum deneme sayısı.

`iter` (`iterator over strings`)
: `pattern` eşleşmeleri arasında `str`'nin her bir bölümü üzerinde bir yineleyici.

{{<example-box>}}

```lua
>>> for str in re.gsplit(",", "a,,b,c") do
>>>     print str
>>> end
a

b
c
```

{{</example-box>}}
{{<example-box>}}

```lua
>>> for str in re.gsplit(",", "a,,b,c", true) do
>>>     print str
>>> end
a
b
c
```

{{</example-box>}}
{{<example-box>}}

```lua
>>> for str in re.gsplit(",", "a,,b,c", false, 1) do
>>>     print str
>>> end
a
,b,c
```

{{</example-box>}}

### re.find

Özet: {{< lua `matches = re.find(str, pattern)` >}}

`str` içinde `pattern` ile eşleşen tüm örtüşmeyen alt dizeleri bul.

`@str` (`string`)
: Desen aranacak dize.

`@pattern` (`string`)
: Aranacak desen. Desendeki yakalama grupları yoksayılır.

`matches` (`table` veya `nil`)
: Tüm eşleşmeler için [Eşleşme Tabloları]({{< relref "re#match-tables" >}}) içeren bir tablo veya hiç eşleşme yoksa `nil`.

{{<example-box>}}

```lua
>>> re.find(".", "☃☃")
{
    {
        ["str"] = "☃",
        ["first"] = 1,
        ["last"] = 3
    },
    {
        ["str"] = "☃",
        ["first"] = 4,
        ["last"] = 6
    }
}
```
{{</example-box>}}

{{<example-box>}}

```lua
function contains_an_a(str)
    if re.find("a", str)
        print "Has an a"
    else
        print "Doesn't have an a"
    end
end
>>> contains_an_a("abc")
Has an a
>>> contains_an_a("def")
Doesn't have an a
```

{{</example-box>}}

### re.gfind

Özet: {{< lua `iter = re.gfind(str, pattern)` >}}

`str` içinde `pattern` ile eşleşen tüm örtüşmeyen alt dizeler üzerinde yineleme yap.

`@str` (`string`)
: Desen aranacak dize.

`@pattern` (`string`)
: Aranacak desen. Desendeki yakalama grupları yoksayılır.

`iter` (`iterator over string, number, number`)
: Her adımda üç değer üreten bir yineleyici: eşleşen dize, kaynak dizedeki eşleşmenin başlangıç indeksi ve kaynak dizedeki eşleşmenin kapsayıcı bitiş indeksi.

{{<example-box>}}

```lua
>>> for str, start_idx, end_idx in re.gfind(".", "☃☃") do
>>>     print string.format("%d-%d: %s", start_idx, end_idx, str)
>>> end
1-3: ☃
4-6: ☃
```

{{</example-box>}}

### re.match

Özet: {{< lua `matches = re.match(str, pattern)` >}}

Bir dizeyle desen eşleştir. Bu, `find` işlevinden farklıdır; çünkü `find` tüm eşleşmeleri döndürür ve alt grupları yakalamaz, `match` ise yalnızca yakalanan alt gruplarla birlikte tek bir eşleşme döndürür.

`@str` (`string`)
: Desen aranacak dize.

`@pattern` (`string`)
: Aranacak desen.

`matches` (`table` veya `nil`)
: Eğer desen dizeyle eşleşmezse `nil`. Aksi takdirde, tam eşleşme için bir [Eşleşme Tablosu]({{< relref "re#match-tables" >}}) ve ardından (varsa) desendeki her bir yakalayıcı alt ifade için bir [Eşleşme Tablosu]({{< relref "re#match-tables" >}}) içeren bir tablo.

{{<example-box>}}

```lua
>>> re.match("(\d+) (\d+) (\d+)", "{250 1173 380}Help!")
{
    {
        ["str"] = "250 1173 380",
        ["first"] = 2,
        ["last"] = 13
    },
    {
        ["str"] = "250",
        ["first"] = 2,
        ["last"] = 4
    },
    {
        ["str"] = "1173",
        ["first"] = 6,
        ["last"] = 9,
    },
    {
        ["str"] = "380"
        ["first"] = 11,
        ["last"] = 13
    }
}
```

{{</example-box>}}

### re.gmatch

Özet: {{< lua `iter = re.gmatch(str, pattern)` >}}

[`re.match`]({{< relref "re#rematch" >}}) işlevinin yineleyici sürümü.

`@str` (`string`)
: Desen aranacak dize.

`@pattern` (`string`)
: Aranacak desen.

`matches` (`iterator over table`)
: Tam eşleşme için (eğer eşleşirse) bir [Eşleşme Tablosu]({{< relref "re#match-tables" >}}) ve ardından (varsa) desendeki her yakalayıcı alt ifade için bir [Eşleşme Tablosu]({{< relref "re#match-tables" >}}) içeren bir tablo döndüren bir yineleyici.

### re.sub

Özet: {{< lua `out_str, rep_count = re.sub(str, replace, pattern, max_count=0)` >}}

`str` içindeki her `pattern` oluşumunu `replace` ile değiştir.

`@pattern` (`string`)
: Aranacak desen.

`@replace` (`string` veya `function`)
: Eşleşmeler için yedek. Bu, eklenen bir dize veya her eşleşme için çağrılan bir işlev olabilir.

  Eğer `replace` bir dizeyse, eşleşmelere referanslar içerebilir. `&` ve `\0` tam eşleşme ile değiştirilir, `\<number>` ise uygun yakalanan alt ifade ile değiştirilir.

  Eğer `replace` bir işlevse, tüm eşleşme için (yakalayıcı alt ifade yoksa) veya her yakalanan alt ifade için çağrılır. İşleve eşleşme dizesi, eşleşmenin başlangıç indeksi ve bitiş indeksi aktarılır. İşlev bir dize döndürürse, eşleşme dönüş değeri ile değiştirilir. Başka bir şey döndürürse, kaynak dize değiştirilmeden bırakılır.

`@max_count` (`number`)
: Sıfırdan büyükse, yapılacak maksimum değişiklik sayısı.

`out_str` (`string`)
: Değişiklikler uygulanmış girdi dizesi.

`rep_count` (`number`)
: Yapılan toplam değişiklik sayısı.

{{<example-box>}}
Tüm \\k örneklerini \\kf ile değiştir:

```lua
>>> re.sub("{\\k10}a{\\k15}b{\\k30}c", "\\\\k", "\\kf")
{\kf10}a{\kf15}b{\kf30}c
```

{{</example-box>}}
{{<example-box>}}
Tüm \\k ve \\K örneklerini \\kf ile değiştir:

```lua
>>> re.sub("{\\K10}a{\\K15}b{\\k30}c", "\\\\k", "\\kf", re.ICASE)
{\kf10}a{\kf15}b{\kf30}c
```

{{</example-box>}}
{{<example-box>}}
Her \\k süresine bir ekle:

```lua
function add_one(str)
    return tostring(tonumber(str) + 1)
end
>>> re.sub("{\\k10}a{\\k15}b{\\k30}c", "\\\\k(\[[:digit:]]+)", add_one)
{\k11}a{\k16}b{\k31}c
```

{{</example-box>}}