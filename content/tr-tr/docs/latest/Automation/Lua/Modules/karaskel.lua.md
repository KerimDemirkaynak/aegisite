---
title: karaskel.lua
menu:
  docs:
    parent: lua-modules
weight: 6261
aliases:
  - /docs/latest/Automation/Lua/Modules/karaskel.lua/
---

Automation 4 `karaskel.lua` içerme dosyası, Automation 4 Lua ile karaoke efektlerinin geliştirilmesine yardımcı olmayı amaçlayan çeşitli işlevler içerir. Ayrıca, Automation 4 Lua'nın kendisi tarafından tanımlananlara ek olarak, yeni veri yapıları ve uzantılar da tanımlar.

`karaskel.lua` dosyasının kendisi [`utils.lua`]({{< relref "util" >}}) ve [`unicode.lua`]({{< relref "unicode" >}}) dosyalarını içerir, bu nedenle `karaskel.lua` kullanırken bunları ayrıca eklemenize gerek yoktur.

Karaoke efektleri oluştururken `karaskel.lua` kullanılması şiddetle tavsiye edilir ve çeşitli metin düzenleme işlevleri içerdiğinden diğer görevler için de yararlı olabilir.

## İşlevler

### karaskel.collect_head

Özet: {{< lua `meta, styles = karaskel.collect_head(subtitles, generate_furigana)` >}}

Tüm başlık bilgilerini ve stil tanımlarını toplamak için altyazı dosyasını okur ve isteğe bağlı olarak furigana düzenleri için yeni stiller oluşturur.

- `subtitles`, Automation 4 Lua tarafından tanımlanan Altyazı Dosyası nesnesidir.
- `generate_furigana` bir boole değeridir: true ise, [furigana düzeni]({{< relref "Furigana_karaoke" >}}) için henüz bir stili olmayan her stil için bir stil oluşturulur. Furigana stillerinin oluşturulması hiçbir zaman mevcut stillerin üzerine yazmaz, çift stil tanımları oluşturmaz veya diğer furigana stilleri için anlamsız furigana stilleri yaratmaz.

`collect_head` çağırmak, genellikle işleme işlevinizde yaptığınız ilk şeylerden biridir.

Döndürülen `meta` tablosu, `[Script Info]` bölümündeki tüm `Ad: Değer` çiftlerinin bir haritasını içerir. Ayrıca, bir veya her iki alanın eksik olduğu durumlarda varsayılan değerler için VSFilter kuralları izlenerek, `PlayResX` ve `PlayResY` alanlarından hesaplanan `meta.res_x` ve `meta.res_y` değerlerini her zaman içerir.

Döndürülen `styles` tablosu, oluşturulan tüm furigana düzeni stilleriyle birlikte tanımlanmış tüm stillerin bir haritasını içerir. Bu tabloda saklanan stil yapıları, kolaylık sağlaması açısından `style.margin_t` için bir takma ad olan `style.margin_v` ek alanına sahiptir. `styles` dizini, stil adlarına (büyük/küçük harfe duyarlı, isimler bozulmamış) ve sayılara göre oluşturulabilir. `styles.n`, saklanan stil sayısıdır ve `styles[1]` tanımlanan ilk stildir.

### karaskel.preproc_line

Özet: {{< lua `karaskel.preproc_line(subtitles, meta, styles, line)` >}}

Tek bir altyazı satırı için boyutlandırma, konumlandırma ve diğer çeşitli bilgileri hesaplar. Bu işlev, sırasıyla `karaskel.preproc_line_text`, `karaskel.preproc_line_size` ve `karaskel.preproc_line_pos` işlevlerini çağırır.

Bu işlev bir değer döndürmez, bunun yerine `line` tablosunu değiştirir. Daha fazla bilgi için aşağıya bakın.

### karaskel.preproc_line_text

Özet: {{< lua `karaskel.preproc_line_text(meta, styles, line)` >}}

Tek bir satırın metnini ön işleme tabi tutar. `meta` ve `styles`, [`karaskel.collect_head`]({{< relref "karaskel.lua.md#karaskelcollect_head" >}}) tarafından döndürülen tablolardır.

Bu işlev bir değer döndürmez, bunun yerine `line` tablosunu değiştirir. Aşağıdaki alanlar eklenir:

- `line.text_stripped` - Tüm geçersiz kılma (override) etiketleri ve vektör çizimleri kaldırılmış satır metni.
- `line.duration` - Milisaniye cinsinden satır süresi.
- `line.kara` ve `line.furi` - Boyut ve konum verileri içermeyen genişletilmiş [karaoke ve furigana tabloları]({{< relref "karaskel.lua.md#karaoke-and-furigana-syllable-tables" >}}).

Bu işlev herhangi bir metin boyutlandırma veya konumlandırma bilgisi hesaplamaz. (Aslında şu anda `meta` veya `styles` argümanlarını hiç kullanmamaktadır.)

### karaskel.preproc_line_size

Özet: {{< lua `karaskel.preproc_line_size(meta, styles, line)` >}}

Bir satır ve tüm karaoke heceleri ile furigana parçaları için boyutlandırma verilerini hesaplar. Ayrıca satır stiline bir referans ekler.

Bu işlev bir değer döndürmez, bunun yerine `line` tablosunu değiştirir. Aşağıdaki alanlar eklenir:

- `line.styleref` - Bu satırın seçili stilini temsil eden Stil tablosuna bir referans.
- `line.furistyle` - Bu satırın furigana düzeni stilini temsil eden Stil tablosuna bir referans. Doğru isme sahip bir stil yoksa, bu alan `false` değerini alır.
- `line.width`, `line.height`, `line.descent` ve `line.extlead` - [`aegisub.text_extents`]({{< relref "../Miscellaneous_APIs#aegisubtext_extents" >}}) tarafından döndürüldüğü şekliyle, ayıklanmış satır metni için boyutlandırma bilgileri.

Ayrıca, bu işlev boyutlandırma bilgileri ekleyerek `line.kara` ve `line.furi` tablolarını değiştirir.

Burada hiçbir konum bilgisi hesaplanmaz.

Eğer `line` tablosu henüz `karaskel.preproc_line_text` ile işlenmemiş gibi görünüyorsa, bu otomatik olarak yapılacaktır.

### karaskel.preproc_line_pos

Özet: {{< lua `karaskel.preproc_line_pos(meta, styles, line)` >}}

Satır, karaoke ve furigana konum bilgilerini hesaplar.

Bu işlev, furigana stili mevcut olmadığında `karaskel.do_basic_layout` işlevini, satır için bir furigana stili tanımlandığında ise `karaskel.do_furigana_layout` işlevini çağırır. Furigana düzeni algoritması, satırın hesaplanan genişliğini değiştirebilir.

Bu işlev bir değer döndürmez, bunun yerine `line` tablosunu değiştirir. Aşağıdaki alanlar eklenir:

- `line.margin_v` - `line.margin_t` için kolay bir takma ad.
- `line.eff_margin_l`, `line.eff_margin_r`, `line.eff_margin_t`, `line.eff_margin_b` ve `line.eff_margin_v` - Satır için etkili kenar boşluğu değerleri. Satır için karşılık gelen kenar boşluğu geçersiz kılma değeri sıfır değilse, o değer kullanılır, aksi takdirde stilde tanımlanan değer kullanılır.
- `line.halign` - `line.styleref.align` değerinden türetilen, satırın yatay hizalaması olan `"left"`, `"center"` veya `"right"` değerlerinden biri.
- `line.valign` - `line.styleref.align` değerinden türetilen, satırın dikey hizalaması olan `"top"`, `"middle"` veya `"bottom"` değerlerinden biri.
- `line.left` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için sol kenar X koordinatı.
- `line.center` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır merkez X koordinatı.
- `line.right` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için sağ kenar X koordinatı.
- `line.top` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için üst kenar Y koordinatı.
- `line.middle` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır dikey merkez Y koordinatı. `line.vcenter` bunun için bir takma addır.
- `line.bottom` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için alt kenar Y koordinatı.
- `line.x` ve `line.y` - Satırın orijinal konumunu elde etmek için bir `\pos` geçersiz kılma etiketinde kullanıma uygun, satır için X ve Y koordinatları.

Ayrıca, `line.kara` ve `line.furi` tabloları, konumlandırma bilgileri eklenerek düzen işlevi tarafından değiştirilir.

Eklenen çeşitli alanlar hakkında daha fazla ayrıntı için bu sayfanın ilerleyen kısımlarındaki [veri yapıları]({{< relref "karaskel.lua.md#data-structures" >}}) bölümüne bakın.

Hiçbir satır boyutlandırma bilgisi bulunmazsa, sırasıyla `karaskel.preproc_line_text` işlevini de çağırabilen `karaskel.preproc_line_size` çağrılacaktır.

### karaskel.do_basic_layout

Bu işlev doğrudan çağrılmak için tasarlanmamıştır, bunun yerine `karaskel.preproc_line_pos` için bir yardımcı işlev olarak çağrılır.

`line.kara` tablosu için çok basit bir düzen algoritması çalıştırır; bu algoritma, aralarında ek boşluk olmadan düz bir çizgide yerleştirildiklerinde hecelerin konumlarını hesaplar. Her karaoke hecesine konumlandırma bilgisi eklenir.

`line.furi` tablosuna dokunulmaz.

### karaskel.do_furigana_layout

Bu işlev doğrudan çağrılmak için tasarlanmamıştır, bunun yerine `karaskel.preproc_line_pos` için bir yardımcı işlev olarak çağrılır.

Karaoke hecelerini ve furiganayı düzgün bir şekilde konumlandırmak ve istenmeyen örtüşmeleri önlemek için gelişmiş bir metin düzenleme algoritması çalıştırır. Kullanılan gerçek algoritma ile ilgilenenler işlev kaynak kodunu okumalıdır. Yeterince yorumlanmış olmalıdır.

Bu işlev hem `line.kara` hem de `line.furi` tablolarına konumlandırma bilgisi ekler. Furigana için yer açmak üzere temel metin genişletildiğinden `line.width` alanını da değiştirebilir.

## Karaoke iskeletleri

Bir karaoke iskeleti, karaoke efektleri oluşturmak için kullanılan bir çerçevedir. Genellikle, gerçek efekt çalışmasını yürütmek için birkaç işlevi kendiniz yazarak çalışır ve bunlar daha sonra çeşitli zamanlarda çağrılır. Yazmanız gereken işlevlerin gerçek ayrıntıları, kullanılan karaoke iskeletine bağlıdır.

### Efekt Kütüphanesi

Ana işlev: `karaskel.use_fx_library_furi(use_furigana, add_macro)`

Bu komut dosyası dosyası için Efekt Kütüphanesi iskeletini kurmak üzere `karaskel.use_fx_library_furi` işlevini çağırın. `script_name` ve `script_description` genel değişkenleri, oluşturulan dışa aktarma filtresini adlandırmak için kullanılır. `use_furigana` true ise, furigana stilleri gerektiği gibi oluşturulur ve eklenir. `add_macro` true ise, dışa aktarma filtresine ek olarak bir makro kaydedilir.

Efekt Kütüphanesi iskeletinin temel varsayımı, her zamanlanmış karaoke satırının Efekt alanında, o satıra hangi efektin uygulanacağını tanımlayan bir kelimenin olmasıdır. Bu, Efekt Kütüphanesi'ni tek bir karaokede birkaç farklı efekt kullanmak istediğinizde iyi bir seçim haline getirir.

Efekt Kütüphanesi çağrıldığında, altyazı dosyasındaki her Diyalog satırı için _fx_effect_ adlı bir işlev çağırır. Örneğin, bir diyalog satırının Efekt alanı _"jump"_ ise, `fx_jump` adlı işlev çağrılır. Efekt alanı boş olan satırlar için `fx_none` işlevi çağrılır.

Bir `fx` işlevi mevcut değilse, orijinal satır altyazı dosyasında bırakılır. Aksi takdirde, orijinal satırın kalıp kalmayacağı `fx` işlevinin dönüş değerine bağlıdır; true bir dönüş değeri orijinal satırın tutulduğu, false bir değer ise satırın Yorum (Comment) satırına dönüştürüldüğü anlamına gelir.

`fx` işlevlerinin imzası: `keep = fx_effect(subtitles, meta, styles, line, fxdata)`

`fxdata`, efektin kullanılacağını tanımlayan ilk kelimeden sonra Efekt alanının içeriğidir. Bir `fx` işlevinin tüm çıktıları `subtitles` tarafından temsil edilen altyazı dosyasına eklenmelidir.

Basitleştirilmiş ana işlev: `karaskel.use_fx_library(add_macro)`

Yukarıdaki `_furi` varyantı ile aynıdır, sadece `use_furigana` parametresi kaldırılmıştır; false olduğu varsayılır.

### Klasik Gelişmiş

Ana işlev: `karaskel.use_classic_adv(use_furigana, add_macro)`

Bu komut dosyası dosyası için Klasik Gelişmiş iskeletini kurmak üzere `karaskel.use_classic_adv` işlevini çağırın. `script_name` ve `script_description` genel değişkenleri, oluşturulan dışa aktarma filtresini adlandırmak için kullanılır. `use_furigana` true ise, furigana stilleri gerektiği gibi oluşturulur ve eklenir, ayrıca furigana işleme etkinleştirilir. `add_macro` true ise, dışa aktarma filtresine ek olarak bir makro kaydedilir.

Bu iskelet, Automation 3 `karaskel-adv` iskeleti imajında oluşturulmuştur ancak onunla uyumlu _değildir_. (Komut dosyanızın bazı bölümlerini yeniden yazmadan `karaskel-adv` betiğini Klasik Gelişmiş ile kullanamazsınız.) Temel varsayım, `do_syllable` işlevinin her hece için bir kez çağrılmasıdır. İsteğe bağlı olarak, `do_line` işlevini kullanarak her satır için bir işlev çağrılmasını sağlayabilirsiniz.

Klasik Gelişmiş, olağan Automation 4 Lua modelinden biraz farklı bir model kullanır. Burada tüm altyazı satırları, daha fazla işleme yapılmadan önce ilk olarak toplanır. Ayrıca, bağlantılı liste tarzı erişime izin vermek için `line.prev` ve `line.next` alanları eklenir. Çıktıya satır eklemek için yine de `subs` nesnesine satır eklemeniz gerekir. İşleme başlamadan önce, tüm orijinal satırlar `subs` nesnesinden _silinir_.

Hece işlevi imzası: `do_syllable(subs, meta, styles, lines, line, syl)`

Hece işlevinin adı _mutlaka_ `do_syllable` olmalıdır. Furigana işleme etkinse, furigana hecelerini işlemek için aynı imzaya sahip `do_furigana` adlı bir işlev de tanımlayabilirsiniz. Furigana burada yine Automation 4 modelini izler.

Satır işlevi imzası: `do_line(subs, meta, styles, lines, line, default_do_line)`

Bir satır işlevi tanımlamak isteğe bağlıdır ve genellikle gerekli değildir. Varsa, satır işlevinin adı _mutlaka_ `do_line` olmalıdır. `default_do_line` parametresi, `do_line` var olmasaydı çağrılacak olan işlevdir. Varsayılan satır işlemesini kendi işlemlerinizle birlikte çalıştırmak için onu çağırabilirsiniz.

## Veri yapıları

`karaskel.lua` birkaç veri yapısını tanımlar ve genişletir. Değişikliklerden bazıları yukarıda bireysel işlevler altında listelenmiştir.

### Stiller dizisi

`styles` dizisi `karaskel.collect_head` işlevi tarafından üretilir ve diğer çoğu `karaskel.lua` işlevine iletilmelidir. Altyazı dosyasındaki tüm stillerin bir listesini içerir ve iki yolla erişilebilir.

`styles.n`, dizideki stil sayısını belirten bir sayıdır. `styles[1]` tanımlanan ilk stildir ve `styles[styles.n]` tanımlanan son stildir.

`styles` dizisi ayrıca, `styles[style.name] == style` olacak şekilde stil adlarına göre de indekslenebilir. İsimler bozulmaz ve indeksleme büyük/küçük harfe duyarlıdır.

`styles` üzerinde değişiklik yapmanın altyazı dosyasını asla güncellemeyeceğini ve buna karşılık altyazı dosyasındaki stilleri güncellemenin de otomatik olarak `styles` içinde yansıtılmayacağını unutmayın.

### Stil tablosu

Bu, temel `style` sınıfı altyazı satırı yapısının hafif bir uzantısıdır.

Bir alan eklenmiştir:

- `style.margin_v`, `style.margin_t` için kolay bir takma addır.

Tam alan listesi:

- `style.class == "style"`
- `style.raw` - Ham satır metni.
- `style.section == "[V4+ Styles]"`
- `style.name` - Stil adı.
- `style.fontname` - Stil tarafından kullanılan yazı tipi yüzünün adı.
- `style.fontsize` - Stil için yazı tipi boyutu.
- `style.color1`, `style.color2`, `style.color3` ve `style.color4` - Normal sırada, stil tarafından kullanılan dört renk. Bunları yönetmek için [`extract_color`]({{< relref "util#extract_color" >}}) ve ailesini kullanın.
- `style.bold` - Kalın/kalın olmayan yazı tipi yüzünü belirtmek için `true`/`false`. Yazı tipi ağırlığını belirtmek için bir sayı da olabilir, ancak bu iyi desteklenmez ve kaçınılmalıdır.
- `style.italic` - Boole, yazı tipi yüzünün italik/eğik bir sürümünün kullanılıp kullanılmadığı.
- `style.underline` ve `style.strikeout` - Boole, metne bu iki dekorasyonun uygulanıp uygulanmadığı.
- `style.scale_x` ve `style.scale_y` - X ve Y yönünde ölçeklendirme, 100 nötrdür.
- `style.spacing` - Metindeki tek tek karakterler arasında piksellerle ek boşluk.
- `style.angle` - Metin için Z ekseni döndürme.
- `style.borderstyle` - Normal ana hatlı metin için 1 (bir), altyazıların arkasındaki opak kutu için 3.
- `style.outline` - Metnin etrafındaki genişletilmiş ana hattın genişliği.
- `style.shadow` - Metnin arkasındaki gölgeye olan mesafe.
- `style.align` - Ekrandaki metin için sayısal tuş takımı tarzı hizalama.
- `style.margin_l`, `style.margin_r`, `style.margin_t` ve `style.margin_b` - Stil için kenar boşlukları. `style.margin_v` üst kenar boşluğu için bir takma addır.
- `style.encoding` - Stil için Windows yazı tipi kodlama kimliği.
- `style.relative_to` - Şu anda desteklenmiyor.
- `style.vertical` - Desteklenmiyor, deneme amaçlı AS5 özelliği.

### Diyalog satırı tablosu

Diyalog satırı sınıfına çok sayıda yeni alan eklenmiştir.

Temel alanlar:

- `line.class == "dialogue"`, yorum satırları için de geçerlidir.
- `line.raw` - Ham satır metni.
- `line.section` - Genellikle `"[Events]"`.
- `line.comment` - Boole, satır Diyalog yerine Yorum satırı ise true.
- `line.layer` - Satır katmanı.
- `line.start_time`, `line.end_time` - Satırın milisaniye cinsinden başlangıç ve bitiş zamanları.
- `line.style` - Satır için kullanılan stilin adı.
- `line.actor` - Satır için oyuncu alanı.
- `line.margin_l`, `line.margin_r`, `line.margin_t` ve `line.margin_b` - Satır için kenar boşluğu geçersiz kılmaları, sıfır değeri stilden kenar boşluğu kullanıldığı anlamına gelir.
- `line.effect` - Satırın Efekt alanı.
- `line.userdata` - Kullanılmamış.
- `line.text` - Diyalog metni.

`karaskel.preproc_line_text` tarafından eklenen temel alanlar:

- `line.text_stripped` - Tüm geçersiz kılma etiketleri ve vektör çizimleri kaldırılmış satır metni.
- `line.duration` - Milisaniye cinsinden satır süresi.
- `line.kara` ve `line.furi` - Sırasıyla genişletilmiş karaoke ve furigana tabloları. Başlangıçta boyut ve konum verileri içermezler.

`karaskel.preproc_line_size` tarafından boyutlandırma için eklenen alanlar:

- `line.styleref` - Bu satırın seçili stilini temsil eden Stil tablosuna bir referans.
- `line.furistyle` - Bu satırın furigana düzeni stilini temsil eden Stil tablosuna bir referans. Doğru isme sahip bir stil yoksa, bu alan `false` değerini alır.
- `line.width`, `line.height`, `line.descent` ve `line.extlead` - `aegisub.text_extents` tarafından döndürüldüğü şekliyle, ayıklanmış satır metni için boyutlandırma bilgileri. `line.width` ayrıca `karaskel.preproc_line_pos` tarafından değiştirilebilir.

`karaskel.preproc_line_pos` tarafından konumlandırma için eklenen alanlar:

- `line.margin_v` - `line.margin_t` için kolay bir takma ad.
- `line.eff_margin_l`, `line.eff_margin_r`, `line.eff_margin_t`, `line.eff_margin_b` ve `line.eff_margin_v` - Satır için etkili kenar boşluğu değerleri. Satır için karşılık gelen kenar boşluğu geçersiz kılma değeri sıfır değilse, o değer kullanılır, aksi takdirde stilde tanımlanan değer kullanılır.
- `line.halign` - `line.styleref.align` değerinden türetilen, satırın yatay hizalaması olan `"left"`, `"center"` veya `"right"` değerlerinden biri.
- `line.valign` - `line.styleref.align` değerinden türetilen, satırın dikey hizalaması olan `"top"`, `"middle"` veya `"bottom"` değerlerinden biri.
- `line.left` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için sol kenar X koordinatı.
- `line.center` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır merkez X koordinatı.
- `line.right` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için sağ kenar X koordinatı.
- `line.top` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için üst kenar Y koordinatı.
- `line.middle` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır dikey merkez Y koordinatı. `line.vcenter` bunun için bir takma addır.
- `line.bottom` - Verilen hizalaması, etkili kenar boşlukları ve çarpışma algılaması olmadığı varsayıldığında satır için alt kenar Y koordinatı.
- `line.x` ve `line.y` - Satırın orijinal konumunu elde etmek için bir `\pos` geçersiz kılma etiketinde kullanıma uygun, satır için X ve Y koordinatları.

Sadece Klasik Gelişmiş iskeleti kullanılırken mevcut olan, bağlantılı liste erişimi için eklenen alanlar:

- `line.prev`, `line.next` - Bundan önceki ve sonraki diyalog satırına erişin. Bunlar ilk/son diyalog satırlarında `nil` olabilir. Boş satırlar, stil satırları, başlık satırları vb. bu bağlantılı listeye _dahil değildir_.

### Karaoke ve furigana hece tabloları

Normal karaoke heceleri ve furigana parçaları için tablolar (hemen hemen) her yönüyle aynıdır ve genellikle sorunsuz bir şekilde aynı kod tarafından işlenebilirler. Aksi belirtilmedikçe, `syl` geçen her yerde bunu `furi` ile değiştirebileceğiniz birkaç nokta vardır.

`aegisub.parse_karaoke_data` tarafından tanımlanan temel alanlar:

- `syl.duration` - Milisaniye cinsinden hece süresi ( `\k` etiketleri için uygun bir sayı elde etmek için 10'a bölün.)
- `syl.start_time`, `syl.end_time` - Hecenin satırın başlangıç zamanına göre milisaniye cinsinden başlangıç ve bitiş zamanı.
- `syl.tag` - Bu heceyi tanımlayan etiket adı, ters eğik çizgi olmadan. Genellikle `k`, `K`, `kf` veya `ko` etiketlerinden biri olacaktır. `kt` etiketinin işlenmediğine dikkat edin. Furigana parçaları, onları tanımlayan orijinal heceyle aynı etikete sahiptir.
- `syl.text` - Hecenin etiketleri içeren metni. Furigana için ayıklanmış metinle aynıdır.
- `syl.text_stripped` - Tüm etiketleri kaldırılmış hece metni. Ana heceler için bu, furigana ve çoklu vurgu parçalarının da kaldırılmış halidir. Genellikle kullanmak isteyeceğiniz metin budur.

`karaskel.preproc_line_text` tarafından eklemeler:

- `syl.kdur` - `\k` etiketlerinde kullanıma uygun, santisaniye cinsinden hece süresi.
- `syl.line` - Bu heceyi içeren satır tablosuna geri referans.
- `syl.inline_fx` - Bu hece için [_inline-fx_]({{< relref "Karaoke_inline-fx" >}}) adı.
- `syl.i` - Bu hecenin indeks numarası.
- `syl.prespace`, `syl.postspace` - Hecenin başlangıcındaki/sonundaki boşluk karakterleri. Furigana için her zaman boştur. Bunlar `syl.text_stripped` içinde yer alan boşluklardır. Genellikle bunlara hiç ihtiyacınız olmaz.
- `syl.text_spacestripped` - Etiketlerden arındırılmış ve baştaki/sondaki boşlukları kırpılmış hece metni. Bu, `syl.prespace` ve `syl.postspace` birlikte `syl.text_stripped` ile aynı şeyi üretebilir. Genellikle bunlara hiç ihtiyacınız olmaz.
- `syl.isfuri` - Tablo bir furigana tablosu ise `true`, değilse `false`. Hem normal hem de furigana hecelerini işlemek için tek bir işlev kullanıyorsanız, yine de farklılaştırılmış işlem yapmak için bunu kullanabilirsiniz.
- `syl.highlights` - Hece için çoklu vurgu verilerinin dizi tablosu. Furigana için tanımlanmış tam olarak bir vurgu vardır. Vurgu tablolarının biçimi için aşağıya bakın.

`karaskel.preproc_line_size` tarafından eklemeler:

- `syl.style` - Bu hece için boyutlandırmayı hesaplamak üzere kullanılan stile referans. Bu, normal heceler için ana satır stili ve furigana için furigana stili olacaktır. Oluşturulan satırların stilini her zaman buna ayarlamalısınız.
- `syl.width`, `syl.height` - `aegisub.text_extents` tarafından döndürüldüğü şekliyle `syl.text_spacestripped` genişliği ve yüksekliği.
- `syl.prespacewidth`, `syl.postspacewidth` - Sırasıyla `syl.prespace` ve `syl.postspace` genişliği. Genellikle bunlara ihtiyacınız olmaz. Furigana için her zaman sıfırdır.

`karaskel.preproc_line_pos` tarafından eklemeler:

- `syl.left`, `syl.center`, `syl.right` - Sırasıyla farklı hizalamalarla kullanım için hecenin/furigananın sol, orta ve sağ hizalanmış konumları. Konumlar _satırın sol kenarına göredir_, yani heceleri ekranda konumlandırmak için bu değerleri kullanmak üzere satır konumlandırması için bir değer eklemeniz gerekeceği anlamına gelir. Bir hece için `syl.right` değerinin bir sonraki hece için `syl.left` değerine eşit olduğuna dair bir garanti yoktur.

{{<example-box>}}

```lua
line.left + syl.center
```

`\an2`, `\an5` veya `\an8` hizalamasıyla kullanıma uygun, bir hecenin varsayılan X konumunu hesaplar.
{{</example-box>}}

#### Vurgu (Highlight) tablosu

Bir vurgu tablosu, çoklu vurgulu zamanlanmış bir hecenin bir vurgusunu tanımlar.

Vurgu tabloları tamamen `karaskel.preproc_line_text` tarafından tanımlanır ve aşağıdaki alanları içerir:

- `hl.start_time`, `hl.end_time` - Satırın başlangıcına göre, milisaniye cinsinden vurgunun başlangıç ve bitiş zamanı.
- `hl.duration` - Milisaniye cinsinden vurgu süresi.