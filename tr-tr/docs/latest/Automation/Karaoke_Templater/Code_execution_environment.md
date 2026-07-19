---
title: Yürütme ortamı
menu:
  docs:
    parent: karaoke-templater
weight: 6160
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Code_execution_environment/
---

Kod bloklarındaki ve kod satırlarındaki Lua kodu, ana betik işlevini yanlışlıkla rahatsız etmeyecek şekilde ayrı bir küresel ortamda çalıştırılır.

Kendi verilerinizi daha sonra kullanmak üzere bu ortamda saklayabilirsiniz; örneğin, kod satırlarında bazı değerleri önceden hesaplayıp daha sonra kod bloklarını kullanarak bunları ekleyebilirsiniz. Ancak bu ortam, efekt şablonları yazmayı kolaylaştırmak için tasarlanmış önceden tanımlanmış birkaç değişken ve işlev de içerir.

Kod yürütme ortamının içeriği ile [satır içi değişkenlerin]({{< relref "./Inline_variables" >}}) ($-değişkenleri) ilişkili olmadığını anlamak önemlidir. Kod yürütme ortamındaki bir şeyi değiştirerek bir satır içi değişkeni değiştiremez veya yenilerini ekleyemezsiniz. Ancak, kod yürütme ortamının içeriğini oluşturabilir ve yeniden tanımlayabilirsiniz.

## Satır ve hece bilgisi

Kod yürütme ortamı, işlenmekte olan mevcut satıra ve hece yapısına işaret eden birkaç değişkenin yanı sıra bazı destekleyici tablolar da içerir. Bunlar sadece [karaskel]({{< relref "../Lua/Modules/karaskel.lua.md#datastructures" >}}) tarafından üretilen yapıların referanslarıdır ve hiçbir şekilde değiştirilmezler.

`line` dışındakilerin hepsini salt okunur olarak kabul etmelisiniz. Diğerlerini değiştirirseniz, kara-templater betiği düzgün çalışmamaya başlayabilir.

- **line** - Şu anda oluşturulmakta olan satır. Bunu değiştirmek, dosyadaki sonuç satırını etkileyecektir. Bkz. **[diyalog satırı tabloları referansı]({{< relref "../Lua/Modules/karaskel.lua.md#dialogue-line-table" >}})**.
- **orgline** - Orijinal satır. Bu, mevcut hecenin üzerinde bulunduğu kaynak satırdır.
- **syl** - Mevcut hece yapısı. Mevcut şablon bir _furi_ şablonuysa, bu mevcut furigana hecesidir. Mevcut şablon _char_ veya _multi_ değiştiricilerinden birine veya her ikisine sahipse, bu bir sözde hece yapısıdır; yani orijinal hece yapısının, işlenmekte olan hecenin mevcut kısmı gibi görünmesi için bazı değerleri değiştirilmiş bir kopyasıdır. Ayrıca bkz. **[hece tabloları referansı]({{< relref "../Lua/Modules/karaskel.lua.md#karaoke-and-furigana-syllable-tables" >}})**.
- **basesyl** - Genellikle `syl` ile aynıdır, ancak şablon _char_ veya _multi_ değiştiricisine sahipse, bu orijinal hecedir. (`syl == basesyl` doğruysa, mevcut şablon ne _char_ ne de _multi_dir.)
- **meta** - Betik hakkında çeşitli meta verileri, yani _Script Info_ bölümünün içeriğini içerir. En önemlisi, betik çözünürlüğünü tanımlayan `res_x` ve `res_y` alanlarına sahiptir.

Tüm bu değişkenler, `meta` hariç, yeni bir satır için işleme başladığında `nil` değerine sıfırlanır. İşleme yeni bir aşamaya geldiğinde ilgili değerlere ayarlanırlar. Bu, örneğin _pre-line_ şablonlarının sadece `line` ve `orgline` değerlerinin ayarlanmış olduğu, `syl` ve `basesyl` değerlerinin ise `nil` olduğu anlamına gelir. _code once_ şablonlarında, `meta` dışındaki tüm değişkenler `nil` değerindedir.

## Standart kütüphaneler ve ilgili şeyler

Hem [**string**](https://www.lua.org/manual/5.1/manual.html#5.4) hem de [**math**](https://www.lua.org/manual/5.1/manual.html#5.6) Lua standart kütüphaneleri, genellikle yararlı oldukları için yürütme ortamına içe aktarılır.

Ayrıca, **`_G`** (alt çizgi büyük G) değişkenini kullanarak kara-templater betiğinin ana yürütme ortamına erişebilir ve bu sayede Lua standart kütüphanesinin geri kalanına ve herhangi bir [yüklenmiş modüle]({{< relref "../Lua/Modules" >}}) erişebilirsiniz. Örneğin, `_G.table.sort` normal `table.sort` işlevine atıfta bulunur. Mevcut kütüphanelerle ilgili ayrıntılar için [Lua 5.1 kılavuzuna](https://www.lua.org/manual/5.1/manual.html#5) bakın.

Geriye dönük uyumluluk için, dahil edilen modüllerin birçoğu ([karaskel.lua]({{< relref "../Lua/Modules/karaskel.lua.md" >}}), [unicode.lua]({{< relref "../Lua/Modules/unicode" >}}) ve [utils.lua]({{< relref "../Lua/Modules/util" >}})) otomatik olarak yüklenir ve varsayılan olarak `_G` aracılığıyla erişilebilir olacaktır. Diğer tüm modüllerin bir kod satırında açıkça `require` ile çağrılması gerekir.

Ayrıca, kod yürütme ortamının kendisine atıfta bulunan bir öz-referans **`tenv`** değişkeni de vardır. Bu, `tenv.tenv == tenv` ifadesinin doğru olduğu anlamına gelir.

## Yardımcı işlevler

Bu işlevler, çıktı satırında (`line` değişkeni) daha karmaşık değişiklikler yapmaya yardımcı olur ve karmaşık efektler oluştururken kaçınılmazdır.

### retime

Özet: `retime(mode, startadjust, endadjust)`

![Retime işlevi açıklaması](/img/3.2/Auto4-kara-templater-retime-explanation.png)

Bu işlev genellikle bir şablonda kendi kod bloğu içinde bir kez kullanılır. Çıktı satırının başlangıç ve bitiş zamanını çeşitli şekillerde ayarlar.

_mode_ parametresi, satırın başlangıç ve bitiş zamanlarının nasıl değiştirileceğini belirler; tırnak içinde verilen aşağıdaki değerlerden biri olmalıdır. Dize olması gerektiğinden, mod adı tırnak işaretleri içine alınmalıdır!

_startadjust_ ve _endadjust_ parametreleri, moda göre anlamlarını biraz değiştirir ancak genellikle mod tarafından kontrol edilen "temel" zamana eklenen milisaniye sayısıdır.

Olası _mode_ değerleri:

- **abs** veya **set** - Hem _startadjust_ hem de _endadjust_ satırın başlangıç ve bitiş zamanını doğrudan ayarlamak için mutlak zaman değerleri olarak kullanılır.
- **preline** - Asıl satır başlangıcından önce gerçekleşen efektler yapmak için tasarlanmıştır. Satırın hem başlangıç hem de bitiş zamanı satırın başlangıç zamanına ayarlanır, ardından _startadjust_ başlangıç zamanına, _endadjust_ ise bitiş zamanına eklenir. Genellikle burada _startadjust_ negatif, _endadjust_ ise sıfır olmalıdır.
- **line** - Normal satır zamanlamalarını kullanır ve sadece başlangıç zamanına _startadjust_, bitiş zamanına ise _endadjust_ ekler.
- **start2syl** - Satırın başından vurgulanana kadar hecenin görünümünü oluşturmak için tasarlanmıştır. Satırın başlangıç zamanı korunur ve bitiş zamanı hecenin başlangıç zamanına ayarlanır. Zamanları kaydırmak için _startadjust_ ve _endadjust_ kullanın.
- **presyl** - _preline_ benzeridir ancak hece zamanlaması içindir.
- **syl** - Hecenin başından sonuna kadar.
- **postsyl** - _presyl_ benzeridir ancak temel zamanlama başlangıç yerine hece bitiş zamanıdır. Burada genellikle sıfır _addstart_ ve pozitif _addend_ kullanmak isteyeceksiniz.
- **syl2end** - Hecenin sonundan satırın sonuna kadar olan süre, _start2syl_ benzeridir.
- **postline** - _postsyl_ benzeridir ancak satır zamanlaması içindir.

Özel bir _mode_ daha vardır:

- **sylpct** - _startadjust_ ve _endadjust_ değerlerinin her ikisi de 0 ile 100 arasında yüzde değerleri olarak ele alınır ve satır zamanlamasını hece süresinin o kısmını kapsayacak şekilde ayarlamak için kullanılır.

_line_ şablonlarında `retime` işlevine dikkat edin. Bunu doğrudan bir _line_ şablonunda kullanırsanız, muhtemelen istediğiniz sonucu vermeyecektir. Sadece _pre-line_, _syl_ ve _furi_ şablonlarında kullanmalısınız. Ayrıca her şablonda yalnızca bir kez kullanmalısınız.

`retime` işlevi her zaman boş dize (`""`) döndürür, bu da kod bloklarında kullanıldığında hiçbir şey çıktılamamasına neden olur, ancak boole ifadelerinde kullanıldığında yine de doğru olarak değerlendirilir.

{{<example-box>}}

```plaintext
template syl: !retime("preline", -1000, 0)!{\pos($scenter,$smiddle)\an5\fscx0\fscy0\t(\fscx100\fscy100)}
```

Bu, heceler için gerçek satır zamanlamasından 1 saniye (1000 milisaniye) önce başlayan bir tür "pop-in" efekti oluşturur. Kodlanacak iki önemli şey: `"preline"` etrafındaki tırnak işaretleri ve başlangıç zamanının geriye taşınması gerektiği için başlangıç ofsetinin negatif (-1000) olması.
{{</example-box>}}
{{<example-box>}}

```plaintext
template syl: !retime("syl", 0, 0)!{\pos($x,$y)\t(\fscx360)}
```

Hecenin vurgulanması sırasında kendi etrafında dönmesini sağlar. _syl_ şablonlarınız `start2syl` ve `syl2end` olarak yeniden zamanlanmadıkça, hece yalnızca vurgulanması sırasında görünecektir. Bir hece satırını sadece hece süresine yeniden zamanlamanın, `\t` etiketinde başlangıç ve bitiş zamanı koyma ihtiyacını nasıl ortadan kaldırdığına dikkat edin; bunlar varsayılan olarak tüm satırın süresine ayarlıdır ve burada satırın süresi hecenin süresidir.
{{</example-box>}}
{{<example-box>}}

```plaintext
template syl: !retime("sylpct", 0, 50)!{\move($x,$y,$x,!$y-10!)}
template syl: !retime("sylpct", 50, 100)!{\move($x,!$y-10!,$x,$y)}
```

Bu iki şablon birlikte, hecenin vurgulanmasının ilk yarısında 10 piksel yukarı, ikinci yarısında ise geri aşağı hareket etmesini sağlar. `retime` kullanmak, aynı heceyi etkileyen birden fazla `\move` etiketi elde etmenin kolay bir yoludur; bir satırda sadece bir `\move` etiketi olabilir, ancak satırı birçok "zincirleme" zamana bölerseniz, aynı hecenin birkaç yönde hareket ettiği bir efekt oluşturabilirsiniz.
{{</example-box>}}

### relayer

Özet: `relayer(newlayer)`

Oluşturulan satırın Katman (Layer) alanını _newlayer_ ile değiştirir.

**Not:** Bir şablonun her zaman sabit bir katman numarasıyla satırlar oluşturmasını istiyorsanız, bu işlevi kullanmanıza gerek yoktur. Şablon satırındaki Katman alanını ayarlamanız yeterlidir; bu, oluşturulan satırlara aktarılacaktır. Bu işlev sadece katman numarası dinamik olduğunda gereklidir.

{{<example-box>}}

```plaintext
template syl: !relayer(syl.i*5+20)!
```

Satırdan oluşturulan her hece giderek daha yüksek bir katman numarası alır. İlk hece 25. katmanda, ikincisi 30. katmanda olur ve bu şekilde devam eder; her hece bir öncekinden 5 daha büyük bir katman alır.
{{</example-box>}}

### restyle

Özet: `restyle(newstyle)`

Oluşturulan satırdaki Stil (Style) alanını _newstyle_ ile değiştirir.

**_Dikkatli olun_**, _bu işlev boyutlandırma ve konumlandırma bilgilerini güncellemez._ `$x`, `$lwidth`, `line.middle` ve `syl.right` gibi boyutlandırma veya konumlandırma bilgileri kullanmak istiyorsanız, aynı yazı tipi adını, yazı tipi boyutunu, kalınlığı, italikliği, yazı tipi kodlamasını, X ve Y ölçeklendirmesini, karakter aralığını, hizalamayı ve kenar boşluklarını kullanan bir stile geçmelisiniz. Bu özelliklerden herhangi birinin farklı olduğu bir stile geçerseniz, konumlandırma ve boyutlandırma bilgileri geçersiz olacaktır.

İşlevin sınırlı kullanımı olduğu için örnek verilmemiştir.

### maxloop

Özet: `maxloop(newmax)`

Bir şablonun kaç kez döngüye alınacağını dinamik olarak kontrol eder.

**_Dikkatli olun_**, _sonsuza kadar döngü yapan bir şablon oluşturmayın._

Bu işlevi kullanmak için şablonlarda döngü (loop) değiştiricisini kullanmanıza gerek yoktur.

{{<example-box>}}

```plaintext
template syl: !maxloop(syl.width + 2*line.styleref.outline)!{\clip(!line.left+syl.left-line.styleref.outline+j-1!,0,!line.left+syl.left-line.styleref.outline+j!,!meta.res_y!)\an5\move(!line.left+syl.center!,!line.middle!,!line.left+syl.center!,!line.middle+math.random(-20,20)!,$start,$end)\shad0}
```

Her heceyi, hecenin boyutuna bağlı olarak bir dizi ince dilime kesin. Her dilim vurgulama sırasında rastgele hareket eder.
{{</example-box>}}
{{<example-box>}}

```plaintext
template syl: !maxloop(j+1)!
```

Sonsuz bir döngü oluşturur. Sürekli olarak `j` değerini bir artırır, böylece döngü asla tamamlanmaz.
{{</example-box>}}

### loopctl

Özet: `loopctl(newj, newmaxj)`

Her iki döngü değişkenini de kontrol eder. Bu işlevin kullanımı şüphelidir.

_newj_ değeri `tenv.j` değişkeninin yeni değerini, _newmaxj_ ise `tenv.maxj` değişkeninin yeni değerini ayarlar.

İşlevin sınırlı kullanımı olduğu için örnek verilmemiştir.

### remember ve recall

Özet:

- `remember(name, value)`
- `remember_if(name, value, condition)`
- `recall(name)`
- `recall(name, default)`

Bu işlev paketi, bir şablonda bir değer hesaplamanıza ve bunu sonraki şablonlarda yeniden kullanmanıza olanak tanır. Bu, özellikle `math.random` işleviyle birlikte kullanıldığında çok yararlıdır, çünkü remember/recall bir şablonda rastgele bir değer seçmenize ve aynı hece için sonraki bir şablonda aynı rastgele değeri kullanmanıza olanak tanır.

_name_, kaydedilen değeri tanımlamak için kullanıcı tarafından seçilen bir isimdir. Bir dize olmalıdır, bu yüzden genellikle tırnak işaretli bir dize sabiti olarak yazılır.

_value_, saklanacak değerdir. Herhangi bir Lua değeri olabilir, ancak dize ve sayı değerleri en kullanışlı olanlardır.

_default_, isimle henüz hiçbir şey saklanmadıysa geri çağrılacak değerdir.

_condition_, değerin gerçekten saklanıp saklanmayacağını kontrol eder.

`remember` ve `remember_if` işlevlerinin her ikisi de verilen _value_ değerini değiştirmeden döndürür. Bu, bir `remember` çağrısını ham değeri koyacağınız herhangi bir yere koyabileceğiniz anlamına gelir.

`remember_if` işlevi, değeri yalnızca verilen _condition_ doğru bir değerse (yani `nil` veya `false` değilse) saklar. Koşul yanlış olsa bile değeri yine de döndürür.

{{<example-box>}}

```plaintext
template syl: {\frz!remember("entryrotation",math.random(100,200))!\fscx300\fscy300\t(0,300,\frz0\fscx100\fscy100)\pos($x,$y)}
template syl: {\frz-!recall("entryrotation")!\fscx300\fscy300\t(0,300,\frz0\fscx100\fscy100)\pos($x,$y)\fad(300,0)}
```

İlk satır 100 ile 200 derece arasında rastgele bir sayı seçer ve seçilen değeri `"entryrotation"` ismiyle saklar. Ardından bu sayıyı bir rotasyon ayarlamak için kullanır ve 0'a dönüştürür, böylece hecenin doğru konumuna dönmesini sağlar.

İkinci satır, geri çağırma için `"entryrotation"` ismini kullandığından aynı sayıyı geri yükler. Önüne bir eksi işareti koyar, ancak aksi takdirde aynı efekti yapar. Sonuç, hecenin iki kopyasının birbirinin tersi yönde, ancak aynı miktarda döndüğü bir efekttir.
{{</example-box>}}
{{<example-box>}}

```plaintext
template syl: {\fscx!remember_if("longsyllables", recall("longsyllables", 100)+10, #syl.duration>200)!}
```

Burada `remember_if` ve `recall`, varsayılan bir değerle birlikte, her kullanıldığında kendini güncelleyen bir değer ayarlamak için birleştirilmiştir.

"longsyllables" ismi en içten geri çağrılmaya çalışılır, ancak henüz mevcut değilse bunun yerine 100 değeri kullanılır. Ardından buna 10 eklenir ve hecenin süresi 200 ms'den uzunsa, değer (geri çağrılan + 10) geri kaydedilir.

Etkisi, "uzun" bir heceyle her karşılaşıldığında tüm heceler için `\fscx` değerinin 10 artmasıdır.
{{</example-box>}}

## Şablon yürütme verileri

Bu değişkenler, yürütülen şablonun durumu hakkında daha fazla bilgi verir veya şablon yürütme kurallarını bir şekilde değiştirir. Genellikle belirli şablon değiştiricileriyle birlikte çalışırlar.

### Döngü şablonları

_loop_ veya _repeat_ değiştiricisine sahip bir şablon çalışırken, kod yürütme ortamında **`j`** ve **`maxj`** olmak üzere iki yeni değişken tanıtılır.

- **maxj**, döngü sayısıdır; yani _loop_ değiştiricisine verilen parametredir.
- **j**, döngü yineleme sayacıdır. İlk yinelemede 1'den başlar ve sonuncusunda _maxj_ olur.

Bir şablon yürütülürken `j` veya `maxj` değerini değiştirirseniz, döngünün yaptığı yineleme sayısını etkileyebilirsiniz. [`maxloop`]({{< relref "Code_execution_environment#maxloop" >}}) işlevi, dinamik döngüler oluşturmak için kullanışlıdır.

{{<example-box>}}

```plaintext
template syl loop 5: {\an5\pos($scenter,$smiddle)\1a&HFF&\3a&Hcc&\t($start,$end,\fscx!100+j\*10!\fscy!100+j\*10!\3a&HFF&)}
```

Hece dolgusu gizlenir, böylece yalnızca kenarlık görünür, ardından döngü yoluyla yalnızca kenarlıktan oluşan satırın birkaç kopyası oluşturulur ve `j` değişkeni kullanılarak farklı, büyüyen boyutlara "patlaması" sağlanır.

Bu örnek, stil tanımının gölgenin devre dışı olduğunu ancak bir kenarlığa sahip olduğunu varsayar.
{{</example-box>}}

{{<example-box>}}

```plaintext
template syl loop 20: {\move($x,$y,!$x+15\*math.cos(math.pi\*2\*j/maxj)!,!$y+15\*math.sin(math.pi\*2\*j/maxj)!,$start,$end)\t($start,$end,\alpha&HFF&)}
```

Burada döngü, 15 yarıçaplı bir [çember üzerindeki birkaç noktayı hesaplamak](https://en.wikipedia.org/wiki/Unit_circle#Trigonometric_functions_on_the_unit_circle) ve hecelerin bunlara doğru hareket etmesini sağlamak için kullanılır. Efekt alanındaki döngü sayısını değiştirerek daha detaylı bir daire yapabilirsiniz çünkü `j/maxj`, toplam döngü sayısının ne kadarının tamamlandığını hesaplamak için kullanılır.
{{</example-box>}}

### fxgroup ile koşullu şablonlar

_fxgroup_ değiştiricisi, bir şablonun yürütülüp yürütülmeyeceğini kontrol etmek için kod yürütme ortamında özel bir **`fxgroup`** tablosu kullanır.

_fxgroup_ değiştiricisine verilen parametre, yürütme ortamındaki `fxgroup` tablosunda bir anahtarı (her zaman bir dize) adlandırır ve bir fxgroup'a atanan bir şablon yürütülmek üzere olduğunda, `fxgroup` tablosundaki o anahtarın değeri aranır. Değer doğruysa veya anahtar mevcut değilse, şablon yürütülür; yanlışsa şablon atlanır.

Fxgroup isimleri için teknik olarak herhangi bir metin dizesi kullanabilseniz de, Lua kodunda kullanıldıkları için `end`, `break`, `return` gibi Lua ayrılmış kelimeleriyle örtüşenlerden kaçınmak en iyisidir.

{{<example-box>}}

```plaintext
code syl: fxgroup.long = (syl.duration > 200)
template syl noblank: all here:
template syl fxgroup long: is long:
karaoke: {\k10}huh? {\k40}wee~~
```

Bu örneği anlamak için şablon yürütme sırasını anlamak önemlidir. Her giriş hecesi için (yani "huh?" ve "wee~~"), tüm şablonlar ve kod satırları göründükleri sırayla çalıştırılır.

Bu, "huh?" için önce kod satırının çalıştırıldığı anlamına gelir. Bu hecenin süresinin 200 ms'den az olduğunu belirler ve böylece _fxgroup.long_ değerini yanlış olarak ayarlar. İlk şablonun fxgroup'u yoktur, bu yüzden o anda heceye uygulanır ve "all here: huh?" satırını çıkarır, ancak ikinci şablonun "long" fxgroup'u vardır. Bu fxgroup, kod satırı tarafından o hece için devre dışı bırakıldığı için o şablon hiç çalıştırılmaz.

"wee~~" için ise kod satırı süresinin 200 ms'den uzun olduğunu belirler, bu yüzden "long" fxgroup etkinleştirilir. Ardından ilk şablon satırını ("all here: wee~~") çıkarır ve ikinci şablon çalıştırılacağı zaman, fxgroup'u etkin olduğu için o da çalıştırılır ve "is long: wee~~" çıktısını verir.

İki şablonun hiçbiri sıfırıncı hece için hiçbir şey çıkarmaz. İlk şablon, "noblank" değiştiricisine sahip olduğu için, ikincisi ise sıfırıncı hecenin süresi fxgroup'un etkinleştirilmesi için çok kısa olduğu için.
{{</example-box>}}