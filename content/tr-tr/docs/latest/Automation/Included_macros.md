---
title: Standart makrolar
menu:
  docs:
    parent: automation
weight: 6500
aliases:
  - /docs/latest/Automation/Included_macros/
---

Aegisub, çeşitli makrolar içerir. İşte bunların bir listesi.

## Karaoke şablonu uygula

Bu, Karaoke Şablonlayıcısı'nın (Karaoke Templater) makro halidir. Bunun nasıl kullanılacağı hakkında bilgi için [Karaoke_Templater]({{< relref "Karaoke_Templater" >}}) sayfasını inceleyin.

Bu makro, yalnızca altyazı dosyasında en az bir şablon satırı olduğunda kullanılabilir.

## Tam genişliğe getir

Tüm ASCII karakterlerini, bunların Japonca "tam genişlik" (full-width) varyasyonlarına dönüştürür.

Bu, karakterlerin "üst üste" gelmesi için bir tabela çevirisini dikey olarak dizmeniz gerektiğinde yararlı olabilir.

Bu makro, altyazı ızgarasında o an seçili olan tüm satırları değiştirir.

{{<example-box>}}
İşte dizilmiş bir tabela:

```ass
{\fn@DFPGothic-EB\fs26\shad0\fe128\bord3\3c&H25485A&\c&HDEEBF1&\pos(456,184)\frz-90}Sign text
```

Bunun bir "@-font" kullandığına dikkat edin; bu, "tam genişlikli" karakterlere sahip her CJK yazı tipinde temel çizgiden 90 derece döndürülmüş olarak bulunan bir varyasyondur. Tam genişlikli karakterler sadece Latin alfabesinin bu tam genişlikli varyasyonlarını değil, aynı zamanda Japonca kana ve kanji, hanzi, hanja ve çeşitli noktalama işaretlerini de içerir.

Şimdi bu makro satır üzerinde çalıştırıldıktan sonra:

```ass
{\fn@DFPGothic-EB\fs26\shad0\fe128\bord3\3c&H25485A&\c&HDEEBF1&\pos(456,184)\frz-90}Ｓｉｇｎ ｔｅｘｔ
```

Makro çalıştırılmadan önce ve sonra görüntüsü şöyledir:

![Üst üste dizilmiş tabela1](/img/3.2/StackedSign1.png) ![Üst üste dizilmiş tabela2](/img/3.2/StackedSign2.png)
{{</example-box>}}

## Otomatik karaoke girişi

Zamanlama açısından birkaç karaoke satırını otomatik olarak birleştirir ve başlarına uygun `\k` etiketlerini ekler.

Bu makro, karaoke efektleri oluşturmaya, özellikle de satırlar için geçişler ve girişler oluşturmaya yardımcı olmak için tasarlanmıştır. Karaoke zamanlaması yapılmış ancak karaoke şablonları gibi efektler henüz uygulanmamış durumlar için oldukça uygundur.

Bu makro, en az iki satırın seçilmesini gerektirir ve yalnızca seçilen her satırın başlangıç zamanı, kendisinden önce gelen seçili satırın başlangıç zamanından büyükse mantıklı bir şekilde çalışır. Seçilen satırların zamanlamasını değiştirir ve ilki hariç hepsinin başlangıcına `\k` etiketleri ekler.

{{<example-box>}}
İşte "sıkı" zamanlanmış iki karaoke satırı:

```ass
Dialogue: 0,0:00:44.46,0:00:46.28,Default,,0000,0000,0000,,{\k15}Ne{\k14}ver {\k14}gon{\k13}na {\k37}give {\k40}you {\k49}up
Dialogue: 0,0:00:46.57,0:00:48.56,Default,,0000,0000,0000,,{\k13}Ne{\k13}ver {\k13}gon{\k13}na {\k36}let {\k46}you {\k65}down
```

Her iki satır da tam olarak ilk kelime söylenmeye başladığında başlar ve son kelime bittiğinde biter.

Şimdi, bu iki satır üzerinde *Otomatik karaoke girişi* makrosu çalıştırılırsa, satırlar şu hale gelir:

```ass
Dialogue: 0,0:00:44.46,0:00:46.28,Default,,0000,0000,0000,,{\k15}Ne{\k14}ver {\k14}gon{\k13}na {\k37}give {\k40}you {\k49}up
Dialogue: 0,0:00:46.28,0:00:48.56,Default,,0000,0000,0000,,{\k29}{\k13}Ne{\k13}ver {\k13}gon{\k13}na {\k36}let {\k46}you {\k65}down
```

İkinci satırın başlangıç zamanı, ilk satırın bitiş zamanıyla eşleşecek şekilde değiştirilir ve bu işlemden kaynaklanan kaymayı telafi etmek için satırın başlangıcına bir `\k` etiketi eklenir. Bu, etkili bir şekilde, giriş (fade-in) ve çıkış (fade-out) efektleri oluşturmak için "boşluk doldurucu" olarak kullanılabilecek boş bir hece yaratır.

Makro ayrıca şu mesajı gösterir:

```plaintext
Smallest inter-line duration: 290 milliseconds
```

Bu sadece, iki satır arasında bulunan en küçük sürenin 290 milisaniye veya 0,29 saniye olduğunu, dolayısıyla her hece vurgusunun tamamen görünür olmasını istiyorsanız, giriş, çıkış ve diğer geçiş efektlerini oluşturmak için elinizde bu kadar zaman olduğunu belirtir.
{{</example-box>}}

## Etiketleri temizle

Bu makro, seçilen tüm satırlardaki geçersiz kılma (override) etiketleri üzerinde çeşitli temizlik işlemleri yapar.

- Yan yana gelen geçersiz kılma bloklarını (yani { ... }) birleştirir (her iki blokta da \\k etiketi varsa, bunlar olduğu gibi bırakılır)
- Geçersiz kılma bloklarındaki tüm \\k etiketlerini en başa taşır (örneğin {\\frz90\\k40} yerine {\\k40\\frz90} yapar). Sıralamayı korumak için tek bir blok içindeki birden fazla \\k etiketine özel dikkat gösterilir
- Satır genelindeki etiketleri (yani etkileri tüm satıra yayılan etiketler -- \\a, \\an, \\org, \\pos, \\move, \\fade, \\fad) satırların başına taşır
- Aynı sınıftan olan satır geneli etiketlerinden, ilki hariç diğerlerini kaldırır (not: \\pos ve \\move aynı sınıftandır; bir satırda yalnızca ilki çalışır, bu nedenle betik ilk \\move veya \\pos etiketini bulur, hangisi önce geliyorsa onu tutar ve diğerlerini kaldırır. Aynı durum \\fad ve \\fade için de geçerlidir)
- Virgülle ayrılmış parametrelerdeki boşlukları kaldırır (örneğin \\pos(200 , 200) ifadesi \\pos(200,200) olur)

Bu makro, bir dışa aktarma filtresi olarak da mevcuttur.

Bu makronun temel amacı, [karaskel.lua]({{< relref "./Lua/Modules/karaskel.lua.md" >}}) dosyasının karaoke satırlarını hece yapılarına daha mantıklı bir şekilde ayırmasını sağlamaktır; örnek için bkz.

Bu makro, ızgarada seçilen tüm satırları değiştirir ve içlerindeki tüm etiket bloklarını yeniden yazar.

{{<example-box>}}
Orijinal satır:

```ass
{\r\frz90\k80}Test {\r\fry180\k60}me
```

Karaskel şu hece yapılarını oluşturur:

- 0 = {\\r\\frz90}
- 1 = Test {\\r\\fry180}
- 2 = me

Satır üzerinde *Etiketleri Temizle* çalıştırıldıktan sonra:

```ass
{\k80\r\frz90}Test {\k60\r\fry180}me
```

Şimdi karaskel şu hece yapılarını oluşturur:

- 0 =
- 1 = {\\r\\frz90}Test
- 2 = {\\r\\fry180}me

Temizlenmiş sürüm genellikle istediğiniz şeydir çünkü geçersiz kılma etiketlerini etkiledikleri hecelerin içine yerleştirir.
{{</example-box>}}

## Kenar bulanıklığı ekle

Seçilen tüm satırlara [`\be1`]({{< relref "../ASS_Tags#bluredges" >}}) ekler. Tüm diyalog satırlarının kenarlarını hafifçe bulanıklaştırmak, [hardsub]({{< relref "Attaching_subtitles_to_video#hardsubbing" >}}) yaparken (özellikle XviD gibi eski kodekler kullanılırken) sıkıştırılabilirliği gözle görülür şekilde artırabilir, ancak format sınırlamaları nedeniyle kenar bulanıklığı stilde ayarlanamaz.

## Etiketleri kaldır

Seçilen satırlardan tüm ASS geçersiz kılma bloklarını ve içindeki etiketleri kaldırır.

## Çakışmaları seç

Başka bir satır aktifken başlayan tüm satırları seçer. Bu, zamanlama hatalarını yakalamak veya okunabilirliği artırmak için bu satırlara alternatif bir stil atamak amacıyla yararlı olabilir.