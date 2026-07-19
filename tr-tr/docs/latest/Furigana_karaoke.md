---
title: Furigana Eğitimi
menu:
  docs:
    parent: tutorials
weight: 2730
aliases:
  - /docs/latest/Furigana_karaoke/
---

![Furigana gösterimi 1](/img/3.2/Furigana-demo-1.png)

_Furigana_ (Aegisub'da genellikle _furi_ olarak kısaltılır), Japonca'da ana metnin yanına yazılan küçük fonetik kılavuz karakterlerini ifade eder. Özellikle ideografik kanji karakterlerinin nasıl okunması gerektiğini belirtmek için hiragana fonetik alfabesini kullanır. Ana metin satırının yanına daha küçük metin yerleştirme işlemine genel olarak [_ruby metni_](https://en.wikipedia.org/wiki/Ruby_character) denir, ancak burada tartışılan uygulama özellikle Japonca furigana düşünülerek tasarlandığından, ruby metni her yerde furigana olarak da adlandırılır.

Aegisub'ın yerel olarak desteklediği hiçbir altyazı formatı ruby metnini veya furigana'yı doğal olarak desteklemez; ancak [karaskel]({{< relref "Automation/Lua/Modules/karaskel.lua.md" >}}) standardı, her bir karakterin konumunu hesaplayarak temel furigana düzenleri oluşturabilen bir algoritma içerir.

Bu sayfa, Automation 4 karaskel.lua betiğinin furigana metni için anladığı sözdizimini ve konumlandırılmış karakterleri fiilen oluşturmak için hesapladığı düzen bilgilerinin nasıl kullanılacağını açıklar.

[Karaoke Templater]({{< relref "Automation/Karaoke_Templater" >}}) da karaskel.lua algoritmasını ve sözdizimini kullanarak furigana desteği uygular.

Sözdiziminin karaoke için tasarlandığını ve [karaoke zamanlamalı]({{< relref "Karaoke_Timing_Tutorial" >}}) metinler etrafında döndüğünü unutmamak önemlidir. Normal metinleri (örneğin diyalog satırları) genel amaçlı ruby metni ile dizgilemek için uygun değildir. Bunun için daha ayrıntılı bir sözdizimi ve daha karmaşık bir düzen motoru gerekecektir.

## Çoklu vurgu (Multi-highlight) sözdizimi

Furigana sözdiziminin ayrılmaz bir parçası için ön koşul, çoklu vurgu sözdizimidir.

Bir hecenin metnini numara işareti (#, ASCII 35, Unicode U+0023) yaparsanız, o hece bir öncekine "katılır": Numara işareti kaldırılır ve iki hecenin zamanlaması toplanarak tek bir hece oluşturulur. Bu şekilde birden fazla zamanlamayı toplayarak arka arkaya birden fazla numara işareti hecesine sahip olabilirsiniz.

Numara işareti hecelerinin bireysel zamanlamaları, oluşturulan hece yapısının [vurgu tablosunda]({{< relref "Automation/Lua/Modules/karaskel.lua.md#highlight-table" >}}) saklanmaya devam eder, ancak hece yapısının ana zamanlaması (`start_time` ve `end_time`), yalnızca numara işareti hecelerinin toplanmış zamanlamalarını yansıtır.

{{<example-box>}}
Bu satır, çoklu vurgu sözdiziminin kanji ve birden fazla heceyi kapsayan kanji gruplarını işaretlemek için nasıl kullanıldığını gösterir:

```ass
{\k5}明日{\k10}#{\k5}#{\k10}ま{\k7}た{\k10}会{\k4}う{\k6}時{\k14}#
```

Aşağıdaki hece yapılarını oluşturur:

<table class="karatable">
    <tr><th>Metin</th><th>Hece süresi</th><th>Vurgu süreleri</th></tr>
    <tr><td rowspan="3">明日</td><td rowspan="3">20</td><td>5</td></tr>
    <tr><td>10</td></tr>
    <tr><td>5</td></tr>
    <tr><td>ま</td><td>10</td><td>10</td></tr>
    <tr><td>た</td><td>7</td><td>7</td></tr>
    <tr><td>会</td><td>10</td><td>10</td></tr>
    <tr><td>う</td><td>4</td><td>4</td></tr>
    <tr><td rowspan="2">時</td><td rowspan="2">20</td><td>6</td></tr>
    <tr><td>14</td></tr>
</table>
{{</example-box>}}

## Temel furigana

Bir heceye furigana eklemek için, ana hece metninden sonra bir dikey çizgi (|, ASCII 124, Unicode U+007C) ve ardından dikey çizgiden sonra furigana metnini eklersiniz. Tek bir ana hecenin furigana'sının birden fazla furigana hecesini kapsamasını sağlamak için tekrar eden hecelere (çoklu vurgu için numara işareti heceleri) de furigana ekleyebilirsiniz.

Arka arkaya birden fazla hecenin furigana'sı olduğunda, bu hecelerin tüm furigana'ları bir araya toplanır ve ait oldukları ana hece dizisinin üzerinde ortalanır. Furigana dizisi ana metinden daha genişse, furigana ana metin ile sola hizalanır. Bu davranışı özel kontrol karakterleri ile kontrol edebilirsiniz, aşağıya bakın.

{{<example-box>}}
Yukarıdaki örneğe furigana eklenmesi:

```ass
{\k5}明日|あ{\k10}#|し{\k5}#|た{\k10}ま{\k7}た{\k10}会|あ{\k4}う{\k6}時|と{\k14}#|き
```

Aşağıdaki heceler, vurgular ve furigana üretilir:

<table class="karatable">
    <tr><th>Metin</th><th>Hece süresi</th><th>Vurgu/furigana süreleri</th><th>Furigana</th></tr>
    <tr><td rowspan="3">明日</td><td rowspan="3">20</td><td>5</td><td>あ</td></tr>
    <tr><td>10</td><td>し</td></tr>
    <tr><td>5</td><td>た</td></tr>
    <tr><td>ま</td><td>10</td><td>10</td></tr>
    <tr><td>た</td><td>7</td><td>7</td></tr>
    <tr><td>会</td><td>10</td><td>10</td><td>あ</td></tr>
    <tr><td>う</td><td>4</td><td>4</td></tr>
    <tr><td rowspan="2">時</td><td rowspan="2">20</td><td>6</td><td>と</td></tr>
    <tr><td>14</td><td>き</td></tr>
</table>
{{</example-box>}}

## Düzeni kontrol etme

Genellikle düz furigana sözdizimi ile üretilen düzen tam olarak istediğiniz gibi olmayabilir veya yanıltıcı olabilir. Bu nedenle, furigana'nın nasıl düzenleneceğini kontrol etmek için kullanılabilecek iki özel karakter vardır.

Bu iki özel karakterin her ikisi de bir hecenin furigana'sının ilk karakterinden önce, yani dikey çizgi karakterinden hemen sonra yerleştirilir.

Birincisi, bir "dizi kesintisi" işaretleyen ünlem işaretidir (!, ASCII 33, Unicode U+0021). Bu, bu hecedeki furigana'nın bir önceki hecenin furigana'sı ile birleşmesini engelleyen görünmez bir ayırıcı görevi görür. Bunu genellikle, her ikisi de furigana'ya sahip olan ancak furigana'larının ayrı olması gereken iki bitişik kanji kelimeniz olduğunda kullanırsınız. Bu durumda, ünlem işaretini ikinci kelimenin ilk hecesinin furigana'sındaki ilk karakter olarak koyun.

Diğer özel karakter, "sola hizalamalı dizi kesintisi" işaretleyen küçüktür işaretidir (<, ASCII 60, Unicode U+003C). Ünlem işareti ile aynı dizi kesintisi anlambilimine sahiptir, ancak taşma davranışını da değiştirir. Küçüktür işaretiyle işaretlenmiş furigana hecesi ile başlayan furigana dizisi, uygulandığı ana metinden daha geniş olduğunda, ana metnin sol kenarından taşması gerekse bile her zaman ana metnin üzerinde ortalanacaktır.

Her durumda, iki furigana dizisi ana metinlerinin ötesine geçecek şekilde çakışırsa, ana metin furigana'lar çakışmayacak şekilde hareket ettirilir.

{{<example-box>}}
İşte düzen kontrolü olmadan ve iki düzen kontrol karakterinin her biriyle gösterilen aynı (oldukça yapay) örnek metin:

| Sonuç | Betik |
| :--- | :--- |
| ![Furigana gösterimi 4](/img/3.2/Furigana-demo-4.png) | `{\k10}`中\|ちゅ`{\k10}`#\|う`{\k10}`国\|ご`{\k10}`#\|く<br>`{\k10}`<u>魂\|た</u>`{\k10}`#\|ま`{\k10}`#\|し`{\k10}`#\|い |
| ![Furigana gösterimi 3](/img/3.2/Furigana-demo-3.png) | `{\k10}`中\|ちゅ`{\k10}`#\|う`{\k10}`国\|ご`{\k10}`#\|く<br>`{\k10}`<u>魂\|!た</u>`{\k10}`#\|ま`{\k10}`#\|し`{\k10}`#\|い |
| ![Furigana gösterimi 2](/img/3.2/Furigana-demo-2.png) | `{\k10}`中\|ちゅ`{\k10}`#\|う`{\k10}`国\|ご`{\k10}`#\|く<br>`{\k10}`<u>魂\|\<た</u>`{\k10}`#\|ま`{\k10}`#\|し`{\k10}`#\|い |

İlk ikisi arasındaki fark sadece birkaç piksel olduğundan aradaki farkı söylemek çok zordur, ancak oradadır. İlk örnekte, た karakteri 魂'un sol kenarından ve 国'un üzerinden biraz taşarken, ikincisinde 魂 ile tam olarak sola hizalanır. İkincisinde, ちゅうごく ayrıca 中国 üzerinde ortalanmıştır, ilkinde ise ortalanmamıştır.
{{</example-box>}}

## Özet

| Karakter | ASCII | Unicode | Nerede | Anlamı |
| :--: | :---: | :--- | :--- | :--- |
| # | 35 | U+0023<br>U+FF03 | Ana metin yerine | Önceki heceyi başka bir vurgu ile genişlet |
| \| | 124 | U+007C<br>U+FF5C | Ana metin ile furigana arası | Bir hecenin ana metnini ve furigana metnini ayır |
| ! | 33 | U+0021<br>U+FF01 | Furigana'nın ilk karakteri | Dizi kesintisi; bu hecenin furigana'sının bir önceki hecenin furigana'sı ile birleşmesini engelle |
| \< | 60 | U+003C<br>U+FF1C | Furigana'nın ilk karakteri | Sola hizalamalı dizi kesintisi; bu hecenin furigana'sının bir önceki hecenin furigana'sı ile birleşmesini engelle, ancak furigana'nın ana metnin soluna taşmasına izin ver |

Her özel karakterin aslında iki farklı Unicode kod noktası ile temsil edilebileceğine dikkat edin. İlki, ASCII karakterine karşılık gelen normal karakterdir, ikincisi (yüksek) kod noktası ise karakterin _tam genişlikli_ (full width) versiyonudur. Genellikle Japonca metni düzenlemek için bir IME (Giriş Yöntemi Düzenleyicisi) kullanırken, tek veya iki normal ASCII karakteri girmek için IME'yi kapatıp tekrar açmaktansa tam genişlik modunda metin girmek daha kolaydır. Bu nedenle, karakterlerin hem yarım genişlikli (ASCII) hem de tam genişlikli versiyonları kabul edilir.

## Karaoke Templater'da Kullanım

Furigana: [_furi_ şablon sınıfı]({{< relref "Automation/Karaoke_Templater/Template_modifiers#furi" >}})

Çoklu vurgu: [_multi_ değiştiricisi]({{< relref "Automation/Karaoke_Templater/Template_modifiers#multi" >}})

{{<example-box>}}
Bu sayfada daha önce kullanılan örneklerin tümü şu kara-templater parçası kullanılarak üretilmiştir:

```plaintext
Comment: 0,0:00:00.00,0:00:00.00,Default,,0000,0000,0000,template syl,{\pos(!line.left+syl.center!,!line.middle!)\an5\k!syl.start_time/10!\k$kdur}
Comment: 0,0:00:00.00,0:00:00.00,Default,,0000,0000,0000,template furi,{\pos(!line.left+syl.center!,!line.middle-line.height!)\an5\k!syl.start_time/10!\k$kdur}
Comment: 0,0:00:00.00,0:00:02.00,Default,,0000,0000,0000,karaoke,{\k15}二|ふ{\k15}#|た{\k10}人|り{\k15}だ{\k57}け{\k5}の{\k6}地|ほ{\k5}球|し{\k8}で
Comment: 0,0:00:02.00,0:00:04.00,Default,,0000,0000,0000,karaoke,{\k10}中|ちゅ{\k10}#|う{\k10}国|ご{\k10}#|く{\k10}魂|<た{\k10}#|ま{\k10}#|し{\k10}#|い
Comment: 0,0:00:04.00,0:00:06.00,Default,,0000,0000,0000,karaoke,{\k10}中|ちゅ{\k10}#|う{\k10}国|ご{\k10}#|く{\k10}魂|!た{\k10}#|ま{\k10}#|し{\k10}#|い
Comment: 0,0:00:06.00,0:00:08.00,Default,,0000,0000,0000,karaoke,{\k10}中|ちゅ{\k10}#|う{\k10}国|ご{\k10}#|く{\k10}魂|た{\k10}#|ま{\k10}#|し{\k10}#|い
```

Kullanılan yazı tipi, furigana 15 punto olacak şekilde MS PMincho 30 punto'dur.
{{</example-box>}}

## Lua betiklerinde kullanım

Her şey [karaskel]({{< relref "Automation/Lua/Modules/karaskel.lua.md" >}}) içerisindedir.

Furigana düzeni, bir satırın ana stili için bir furigana stili varsa `karaskel.preproc_line_pos` tarafından otomatik olarak çağrılır. Bir ana stilin furigana stili, ismin sonuna `-furigana` eklenmiş aynı isimdeki stildir. Örneğin, `Default` stilinin furigana stili `Default-furigana`'dır.

Karaskel, `karaskel.collect_head` fonksiyonunun `generate_furigana` argümanı (ikinci) `true` ise otomatik furigana stilleri oluşturabilir. Otomatik furigana stilleri, yazı tipi boyutunun yarıya indirilmesi dışında temel aldıkları ana stil ile aynıdır.

Furigana heceleri `line.furi` içinde saklanır ve normal hecelerle aynı formatı izler. Oluşturduğunuz satırların stilini furigana stiline ayarlamayı unutmamalısınız.

Çoklu vurgular, furigana düzeni yapılmadığında bile her zaman işlenir. Çoklu vurgu verileri `syl.highlights` içinde saklanır.

{{<todo>}}daha fazla ayrıntı {{</todo>}}