---
title: Değiştiriciler
menu:
  docs:
    parent: karaoke-templater
weight: 6130
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Template_modifiers/
---

Şablon satırları ve kod satırları bir dizi değiştirici alabilir.

Bu, `template` veya `code` anahtar kelimesini takip eden, Effect (Efekt) alanındaki boşlukla ayrılmış bir kelime listesidir.

Değiştiriciler bir dereceye kadar birleştirilebilse de, hepsi birbiriyle uyumlu değildir ve hepsi hem kod satırlarında hem de şablonlarda çalışmaz.

Şablon satırının veya kod satırının sınıfını bildiren özel bir değiştirici seti vardır.

## Sınıf bildiren değiştiriciler

Hem şablon satırları hem de kod satırları, bir sınıf değiştiricisi olmadan da oluşturulabilir. Ancak netlik açısından bir tane kullanılması önerilir.

Sınıf değiştiricisi olmayan bir şablon satırına örtük olarak `syl` değiştiricisi verilir.

Sınıf değiştiricisi olmayan bir kod satırına örtük olarak `once` değiştiricisi verilir.

### once

Bu sınıf değiştiricisi yalnızca kod satırları için geçerlidir.

`once` değiştiricisine sahip kod satırları, Karaoke Templater yürütme işlemi sırasında tam olarak bir kez çalıştırılır ve her zaman diğer tüm kod satırlarından veya şablonlardan önce çalıştırılır. Bildirildikleri sırayla çalıştırılırlar.

"code once" satırları öncelikli olarak şablonlarda kullanılacak işlevleri tanımlamak için tasarlanmıştır.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>code once</u>,function setlayer(newlayer) line.layer = newlayer; return ""; end
```

Bu örnek, çıktı satırındaki Layer (Katman) alanını değiştiren yeni bir işlev tanımlar.
{{</example-box>}}

### line _\[isim\]_

Bu sınıf değiştiricisi hem kod satırları hem de şablon satırları için geçerlidir.

Şablon satırlarında kullanıldığında, şablon satırının dahil olduğu satır şablonunu adlandıran isteğe bağlı bir parametre alır. Şablon ismi, hiçbir şablon değiştirici ismiyle eşleşmemelidir.

İsimsiz satır şablonları (hiçbir şablon ismi verilmemiş olanlar), satır öncesi şablon metnine sahip olamaz.

Kod satırları adlandırılamaz, isimsiz olmaları gerekir.

İsimlendirilmiş satır şablon satırları, göründükleri sırayla şablon metnine eklenir. Şablon metninin eklenmesi, yürütme sırasında değil, şablon ayrıştırma (parse) sırasında gerçekleşir.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>code line</u>,fxgroup.funky = line.actor == "funky"
```

Bu kod satırı, her giriş satırı için bir kez çalıştırılır. Giriş satırının Actor (Oyuncu) alanına bağlı olarak "funky" adlı bir efekt grubunu etkinleştirir/devre dışı bırakır.
{{</example-box>}}
{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template line</u>,{\r\t($start,$end,\bord0)}
```

Bu şablon satırı, isimsiz bir satır şablonu bildirir. Oluşturulan efekt, hecenin süresi boyunca her hecenin kenarlığını sıfıra dönüştürecektir.
{{</example-box>}}
{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template line jumper</u>,{\r\t($start,$mid,\frz-0.1)\t($mid,$end,\frz0}
```

Bu şablon satırı "jumper" adlı bir satır şablonuna ekleme yapar veya mevcut değilse oluşturur. Aşağıda verilen satır öncesi (pre-line) şablon örneğiyle birlikte, bu heceler için bir "zıplama" efekti oluşturacaktır.
{{</example-box>}}

### pre-line _\[isim\]_

Bu sınıf değiştiricisi yalnızca şablon satırları için geçerlidir.

`pre-line` değiştiricisi, şablon satırının dahil olduğu satır şablonunu adlandıran isteğe bağlı bir parametre alır. Şablon ismi, hiçbir şablon değiştirici ismiyle eşleşmemelidir.

Yalnızca pre-line (satır öncesi) metnine sahip isimsiz satır şablonları, orijinal giriş satırı metnini olduğu gibi bırakır ve şablon metnini sadece satırın başına ekler.

İsimlendirilmiş pre-line şablon satırları, göründükleri sırayla pre-line şablon metnine eklenir. Şablon metninin eklenmesi yürütme sırasında değil, şablon ayrıştırma sırasında gerçekleşir.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template pre-line</u>,{\be1}
```

Bu şablon satırı, eşleşen tüm satırların başına `{\be1}` ekleyecek isimsiz bir satır şablonu bildirir.
{{</example-box>}}
{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template pre-line jumper</u>,{\org(-10000,$y)}
```

Bu şablon satırı, "jumper" adlı bir satır şablonunun pre-line şablon metnine ekleme yapar veya mevcut değilse oluşturur. Yukarıda verilen satır şablonu örneğiyle birlikte, bu heceler için bir "zıplama" efekti oluşturacaktır.
{{</example-box>}}

### syl

Bu sınıf değiştiricisi hem kod satırları hem de şablon satırları için geçerlidir.

Syl şablonları adlandırılamaz.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template syl</u>,{\pos($x,$y)}
```

Bu şablon satırı, hece metnini basitçe konumlandıran bir syl şablonu bildirir.
{{</example-box>}}

### furi

Bu sınıf değiştiricisi hem kod satırları hem de şablon satırları için geçerlidir.

Furi şablonları adlandırılamaz.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template furi</u>,{\pos($x,$y)}
```

Bu şablon satırı, hece metnini basitçe konumlandıran bir furi şablonu bildirir. Doğru furigana biçimlendirmesi elde etmek için başka bir şey yapılmasına gerek yoktur.
{{</example-box>}}

### syl furi

`syl` ve `furi` sınıf değiştiricilerini birleştirmek mümkündür. Bu, şablon satırından iki özdeş şablonun (bir syl şablonu ve bir furi şablonu) oluşturulmasıyla sonuçlanır.

Bu, sınıf değiştiricilerinin tek olası kombinasyonudur, aksi takdirde birbirlerini dışlarlar.

## Diğer değiştiriciler

### all

Şablonu yalnızca şablon satırının stiline değil, tüm stillere uygular.

Hem kod satırları ve şablonlar hem de tüm sınıflar için uygulanabilir.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template syl all</u>,{\pos($x,$y)}
```

Bu şablon, satırın sahip olduğu stilden bağımsız olarak, tüm altyazı dosyasındaki her bir heceye uygulanacaktır.
{{</example-box>}}

### char

Şablonun hece başına değil, karakter başına çalışmasını sağlar. Bu, uygulama sırası semantiğini önemli ölçüde değiştirir, ayrıntılar için [Şablon yürütme ve sırası]({{< relref "./Template_execution_rules_and_order" >}}) bölümüne bakın.

Bu kod satırlarında çalışsa da, genellikle kullanışlı değildir; yürütme sırası hakkındaki tartışmaya bakın.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template syl char</u>,{\pos($x,$y)}
Comment: 1,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template syl char</u>,{\pos($x,$y)\bord0}
```

Satırdaki her bir karakter ayrı ayrı konumlandırılacaktır. Her hece için, her şablon tüm karakterlere bir kerede uygulanacak ve birbirine geçmeli olarak uygulanmayacaktır.

Örneğin, "ab" ve "cd" şeklinde iki hece varsa ve yukarıdaki iki şablon bunlara uygulanırsa, sonuç şu sırada aşağıdaki metne sahip 8 satır olacaktır:

```ass
{\pos($x,$y)}a
{\pos($x,$y)}b
{\pos($x,$y)\bord0}a
{\pos($x,$y)\bord0}b
{\pos($x,$y)}c
{\pos($x,$y)}d
{\pos($x,$y)\bord0}c
{\pos($x,$y)\bord0}d
```

{{</example-box>}}

### fx _name_

Şablonun yalnızca adlandırılmış [satır içi efektlere (inline-fx)]({{< relref "Karaoke_inline-fx" >}}) sahip hecelere uygulanmasını sağlar. Bir satır içi efekt ismi belirtmek zorunludur; ismin şablon değiştirici isimleriyle çakışabileceği durumlar olabilir ancak bu önerilmez.

{{<example-box>}}

```plaintext
Comment: 0,0:00:00.00,0:00:05.00,Default,,0000,0000,0000,<u>template syl fx drop</u>,{\move($x,$y,$x,!$y+30!,$start,$end)}
```

Bu şablonla, "drop" satır içi efektine sahip tüm heceler için, hecenin süresi boyunca 30 piksel aşağı hareket ettiği ek bir satır üretilir.

_fx_ belirtilmemiş diğer tüm şablon satırları da bu hecelere her zamanki gibi uygulanmaya devam edecektir.
{{</example-box>}}

### fxgroup _name_

Şablonun adlandırılmış efekt grubunda olduğunu bildirir. Bir efekt grubu ismi belirtmek zorunludur; ismin şablon değiştirici isimleri ve Lua'nın ayrılmış kelimeleriyle çakışabileceği durumlar olabilir ancak bu önerilmez.

{{<example-box>}}
[Kod yürütme ortamı]({{< relref "./Code_execution_environment#conditional-templates-with-fxgroup" >}}) sayfasında bir _fxgroup_ örneği bulunmaktadır.
{{</example-box>}}

### keeptags

Uygulamadan sonra orijinal etiketlerin hecede tutulması gerektiğini belirtir.

Bunun `char` veya `multi` ile birleştirildiğinde bir etkisi yoktur.

{{<example-box>}}

```plaintext
template line <u>keeptags</u>: {\r\t($start,!$start+1!,\frx40)\t(!$start+1!,$end,\frx0)}
karaoke: {\k21}hi{\k10}gu{\k23}ra{\k22}shi {\k38}ga {\k37\1c&H0000FF&}na{\k37}ku
```

Heceler vurgu sırasında biraz geriye doğru "eğilir". Bir tanesi ("na"), zamanlanmış karaoke satırına bir geçersiz kılma etiketi konularak farklı renklendirilir, ancak şablonun başındaki alışılagelmiş `\r` nedeniyle sonraki heceler bunu almaz.

_notags_ değiştiricisi, özel hecenin özel renginin çıktıya taşınmasını sağlar.
{{</example-box>}}

### multi

Şablonun [çoklu vurgulama (multi-highlight)]({{< relref "Furigana_karaoke" >}}) zamanlanmış karaokede, vurgu başına uygulanmasını sağlar. Bu, uygulama sırası semantiğini önemli ölçüde değiştirir, ayrıntılar için [Şablon yürütme ve sırası]({{< relref "./Template_execution_rules_and_order" >}}) bölümüne bakın.

Bu kod satırlarında çalışsa da, genellikle kullanışlı değildir; yürütme sırası hakkındaki tartışmaya bakın.

{{<example-box>}}

```plaintext
template syl <u>multi</u>: {\an5\pos($scenter,$smiddle)\1a&HFF&\t($start,$end,\bord5\3a&HFF&)}
karaoke: {\k33}風<u>{\k36}#</u>{\k89}の{\k46}花<u>{\k28}#</u>{\k57}よ
```

Zamanlanmış karaoke satırı, çoklu vurgulama heceleri oluşturmak için temel çoklu vurgulama işaretlemesi olan `#` hecelerini kullanır. Bu şekilde, 風 (ka-ze) ve 花 (ha-na) kanjilerinin her biri, her biri iki vurgu alan tek bir hece olarak depolanır ve `#` karakterleri uygulanan efektte hiç görüntülenmez. (Zamanlanmış karaoke satırını hiçbir şablon uygulamadan oynatırsanız yine de görüntülenirler.)

Şablon, görüntülenen hece başına sadece bir vurgu/uygulama yerine çoklu vurgulamaları kullanmak istediğini belirtmek için _multi_ değiştiricisini kullanır. Efekt, bir çeşit basit "patlayan kenarlık" etkisidir ancak hem 風 hem de 花 kanjilerinde iki kez patlar. Eğer _multi_ değiştiricisi olmasaydı, her birinde sadece bir kez patlardı.
{{</example-box>}}

### noblank

Şablonun "boş" kabul edilen hecelere uygulanmayacağını belirtir. Etiketlerden arındırılmış metni yalnızca ASCII boşluk karakterleri ve ideografik tam genişlikli boşluk karakterleri kombinasyonundan oluşuyorsa veya tamamen boşsa, bir hece boş kabul edilir. Bir hece, süresi sıfır ise yine boş kabul edilir.

> _Bir örnek için aşağıdaki _notext_ değiştiricisine bakın._

### notext

Orijinal metnin çıktı satırına eklenmeyeceğini belirtir.

Bu, öncelikli olarak çizim (drawing) etiketleri ve benzerlerini çıktılayan şablonlarla kullanım için tasarlanmıştır.

Kod satırları için uygulanamaz.

{{<example-box>}}

```plaintext
code once: sword_shape = "m 0 0 l 5 -5 l 5 -30 l 10 -30 l 10 -32 l 2 -32 l 2 -40 l -2 -40 l -2 -32 l -10 -32 l -10 -30 l -5 -30 l -5 -5 "
template syl notext noblank: {\an5\move($scenter,!$smiddle-30!,$scenter,$smiddle,!$start-20!,$start)\p2}!sword_shape!
```

İlk kod satırı, kolaylık sağlaması için bir vektör çizim şekli tanımlar, böylece daha sonraki şablon satırlarını karıştırmaz. Çizim, aşağıya doğru işaret eden küçük, basit bir kılıçtır. Efektin kendisi, bir hareket (move) komutu ile hecelerin üzerine düşen bu küçük kılıçlardır.

Şablon, orijinal hece metninin gösterilmesini önlemek için _notext_ değiştiricisini kullanır, çünkü burada bir vektör çizimi ile değiştirilmektedir. Ayrıca, "görünmez" heceler için herhangi bir şey üretmemek adına _noblank_ değiştiricisi kullanılır; örneğin, tek başına zamanlanmış bir boşluğun üzerine düşen bir kılıç görmek istemeyiz, bu sadece saçma görünür.
{{</example-box>}}

### repeat _n_, loop _n_

Şablonun belirtilen sayıda uygulanacağını belirtir. Döngü sayısını belirtmek zorunludur. Döngü sayısı sabit bir tam sayı olmalıdır; değişken olamaz veya dinamik olarak hesaplanamaz.

`repeat` ve `loop` eş anlamlıdır.

Döngüye alınmış satır şablonlarının ve döngüye alınmış syl/furi şablonlarının yürütme sırasının farklı olduğuna dikkat edin. Ayrıntılar için [Şablon yürütme ve sırası]({{< relref "./Template_execution_rules_and_order" >}}) bölümüne bakın.

{{<example-box>}}

```ass
template syl <u>loop 4</u>: {\move($x,$y,!$x+math.random(-30,30)!,!$y+math.random(-30,30)!,$start,$end)\alpha&Hc0&\t($start,$end,\alpha&HFF&)}
```

_loop_ değiştiricisi, bu şablon her çalıştırıldığında hecenin 4 kopyasını oluşturmak için kullanılır. Bunların her biri, X ve Y yönünde 30 piksele kadar rastgele bir yöne hareket eder. Ayrıca solarak kaybolurlar.

Her kopya için başlangıç alfası olan `&Hc0`, 256 - (256 / 4) olarak seçilmiştir, 4 yapılan döngü sayısıdır. Bu şekilde, her kopyanın opaklığı toplamda tam olarak 256'ya ulaşır. (Teknik olarak 255 olmalıdır, ancak bu çift döngü sayısı ile elde edilemez.)
{{</example-box>}}

> _Daha gelişmiş kullanımlar için [Kod yürütme ortamı]({{< relref "./Code_execution_environment#loopingtemplates" >}}) sayfasındaki örneklere de bakın._