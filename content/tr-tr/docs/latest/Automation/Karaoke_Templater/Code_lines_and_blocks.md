---
title: Kod satırları ve blokları
menu:
  docs:
    parent: karaoke-templater
weight: 6150
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Code_lines_and_blocks/
---

Karaoke Templater'daki kod satırları ve blokları, küçük Lua kodu parçacıklarını dahil ederek gelişmiş efektler oluşturmanıza olanak tanır. Bu, iki sayıyı toplayan basit matematiksel ifadelerden, örneğin döngüsel renklerle çeşitli şekiller üretebilen karmaşık işlevlere kadar uzanabilir.

Hem kod satırları hem de kod blokları ayrı, yarı kapalı bir yürütme ortamında çalıştırılır; bu, Karaoke Templater betiğinin kendisinin çalıştığı birincil Lua ortamından büyük ölçüde etkilenmedikleri anlamına gelir. Kod satırı/bloğu yürütme ortamında hangi değişkenlerin mevcut olduğuna dair bir genel bakış için bkz: [Kod yürütme ortamı]({{< relref "./Code_execution_environment" >}}).

## Kod satırları

Kod satırı, özel bir şablon satırı türüdür. Effect (Efekt) alanında `template` anahtar kelimesini kullanmak yerine `code` anahtar kelimesini kullanır. Bir kod satırı yalnızca Lua kodu içerir ve tek başına sonuç dosyasında herhangi bir satır üretmez.

Kod satırlarının iki temel kullanım amacı şunlardır:

- Şablonlarda daha sonra kullanılmak üzere değişkenleri tanımlamak/güncellemek
- Şablonlarda daha sonra kullanılmak üzere işlevler tanımlamak

Örneğin, rastgele bir sayıya ihtiyacınız varsa, ancak bunu bir şablonda iki kez kullanmanız gerekiyorsa, önce sayıyı üretip bir değişkene kaydetmek için bir kod satırı kullanabilir, ardından bu değişkeni şablon satırınızda kullanabilirsiniz.

Bir başka örnek, rastgele bir renk üreten bir işlev tanımlamak olabilir.

### Kod satırı sınıfları

Birden fazla şablon satırı sınıfı olduğu gibi, birden fazla kod satırı sınıfı da vardır. Bunların bazıları aynıdır, bazıları ise sadece biri veya diğeri için mevcuttur.

Kod satırının sınıfını, Effect (Efekt) alanında `code` anahtar kelimesinden sonra belirtirsiniz. Olası sınıflar şunlardır:

once
: `once` sınıfındaki kod satırları, şablonlar uygulanmadan önce tam olarak bir kez çalıştırılır. Burası genellikle işlevleri ve daha sonra aramanız gereken genel değer tablolarını tanımlamak için en iyi yerdir. Bu varsayılan sınıftır; bir kod satırı için sınıf belirtmezseniz otomatik olarak `once` sınıfına dahil edilir.

line
: `line` sınıfındaki kod satırları, yeni bir satırla karşılaşıldığında çalıştırılır. Satır başına bir kez çalışırlar. Göründükleri sırayla `line`/`pre-line` şablonları arasına serpiştirilmiş şekilde çalışırlar. ("pre-line" kod satırı yoktur.)

syl
: `syl` sınıfındaki kod satırları, yeni bir heceyle karşılaşıldığında çalıştırılır. Hece başına bir kez çalışırlar. `syl` şablonları arasına serpiştirilmiş şekilde çalışırlar.

furi
: `furi` sınıfındaki kod satırları, yeni bir furigana hecesiyle karşılaşıldığında çalıştırılır. Furigana hecesi başına bir kez çalışırlar. `furi` şablonları arasına serpiştirilmiş şekilde çalışırlar.

`char` veya `multi` değiştiricilerine sahip şablonların, kod satırlarıyla iç içe geçmiş şekilde karakter başına/vurgu başına çalışmasını sağlayamazsınız. Bu, yürütme modelinin bir kısıtlamasıdır. Bu durum Karaoke Templater'ın sonraki sürümlerinde değişebilir veya değişmeyebilir.

## Kod blokları

Kod bloğu, bir şablon satırı içindeki Lua kodu bloğudur. Kod blokları, [satır içi değişkenlerle]({{< relref "./Inline_variables" >}}) ifade edilebilecek olandan daha karmaşık şeyleri eklemek için kullanılır.

Kod bloklarına otomatik olarak bir `return` ifadesi eklendiğinden, tek bir Lua ifadesi olmaları gerekir. Bu, diğer şeylerin yanı sıra kod blokları içinde atama yapamayacağınız veya `if` ifadeleri kullanamayacağınız anlamına gelir; bu tür işlemleri yapmak istiyorsanız bir kod satırı kullanmalısınız. (Yine de kod bloklarında temel koşullu ifadeler kullanmanın bir yolu vardır, aşağıya bakın.)

Kodu ünlem işaretleriyle çevreleyerek bir kod bloğu oluşturursunuz, şöyle:

```ass
{\t($start,!syl.start_time+20!,\bord0)}
```

Kod blokları içinde satır içi değişkenleri kullanmak mümkündür. Kod bloğu ayrıştırılmadan önce genişletilirler, bu nedenle Lua yorumlayıcısı için satır içi değişkenler normal sabitler gibi görünür.

### Kod bloklarını kullanmak için ipuçları

Çoğu basit matematiksel ifade tam beklediğiniz gibi çalışır. Operatör öncelik kuralları, normal aritmetik kurallarıdır.

Bir kod bloğu her zaman bir dizge (string) veya sayısal değer döndürmelidir; boolean, tablo veya başka bir şey döndürürse bir uyarıya ve yanlış çıktı içeren sonuç satırına neden olabilir.

Kod blokları içinde basit koşullu ifadeler oluşturmak için değerleri ve koşulları zincirlemek üzere `and` ve `or` operatörlerini kullanabilirsiniz. Örneğin:

```ass
{\k!syl.duration > 100 and "f" or ""!$kdur}
```

Eğer hece süresi 100 ms'den uzunsa ilk alt ifade doğru olur ve kod bloğu `"f"` döndürür; aksi takdirde tüm `and` ifadesi yanlış olur ve `or` ifadesinin sağ tarafındaki argüman döndürülür.

Lua'da `and`, `or` operatöründen daha güçlü bağlandığı için `and` ifadeleri önce değerlendirilir. Yukarıdaki ifadede etkili gruplandırma şu şekildedir:
`((syl.duration > 100) and "f") or ""`