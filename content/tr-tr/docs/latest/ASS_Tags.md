---
title: ASS Geçersiz Kılma (Override) Etiketleri
menu:
  docs:
    parent: typesetting
weight: 4400
aliases:
  - /docs/latest/ASS_Tags/
---

Aşağıdaki liste, Advanced Substation Alpha formatı tarafından desteklenen tüm etiketleri içermektedir. Bu belge, ass-quickref.txt dosyasının detaylı bir versiyonudur. Dizgi (typesetting) işlemlerine giriş ve temel etiketlerin kullanımı için [eğiticiye]({{< relref "Visual_Typesetting" >}}) göz atın.

## Özel karakterler

Aşağıdaki etiketler geçersiz kılma bloklarının (yani { ve } arası) dışında, doğrudan metnin ortasına yazılır.

{{<tag-def-box title="Soft line break" id="\n">}}\n{{</tag-def-box>}}
Zorunlu bir satır sonu ekler, ancak yalnızca kaydırma modu 2'de çalışır. (Bkz: [\q etiketi]({{< relref "ASS_Tags#\q" >}})). Bunun küçük harf 'n' olduğuna dikkat edin.

Diğer tüm kaydırma modlarında bu etiket, normal bir boşlukla değiştirilir. Bu karakterin kullanımı nadirdir (eğer kullanılıyorsa). \n ile \N arasında hangisini kullanacağınızdan emin değilseniz, büyük ihtimalle \N kullanmak istiyorsunuzdur.

{{<tag-def-box title="Hard line break" id="\N">}}\N{{</tag-def-box>}}
Kaydırma modundan bağımsız olarak zorunlu bir satır sonu ekler. Bunun büyük harf 'N' olduğuna dikkat edin.

{{<tag-def-box title="Hard space" id="\h">}}\h{{</tag-def-box>}}
Satır bölünmesini engelleyen bir "sert" boşluk ekler. Satır, sert boşluğun hemen öncesinde veya sonrasında otomatik olarak bölünmez ve görüntülenen bir satırın başında veya sonunda yer aldıklarında bu boşluklar yok sayılmaz.

## Geçersiz kılma (Override) etiketleri

Geçersiz kılma etiketleri, { ile başlayıp } ile biten blokların içinde bulunmalıdır. Geçersiz kılma blokları içindeki tanınmayan metinler sessizce yoksayılır, bu yüzden genellikle satır içi yorumlar için de kullanılırlar. Yorumlar ile geçersiz kılma etiketlerini aynı blok içinde karıştırmanız önerilmez.

Etiketler genel olarak iki kategoriye ayrılır: Satırın kendisine ait bir özelliği belirleyenler ve sadece kendilerinden sonra gelen metni değiştirenler. `\pos`, `\move`, `\clip`, `\iclip`, `\org`, `\fade` ve `\fad` ilk kategoriye girer; diğerleri ise ikinci kategoriye aittir. İlk kategorideki etiketler bir satırda en fazla bir kez kullanılmalı ve satırın neresinde oldukları önemsizdir. Ayrıca, bazıları birbiriyle çelişir: `\pos` ve `\move`; `\clip` ve `\iclip`; `\fad` ve `\fade`. Bu etiketlerin veya çelişkili etiketlerin birden fazla kez kullanımının sonuçları oluşturucudan oluşturucuya farklılık gösterir ve önerilmez.

İkinci kategorideki etiketler, satır sonuna kadar veya özellik başka bir etiketle tekrar geçersiz kılınana kadar takip eden tüm metni değiştirir.

Geçersiz kılma etiketleri her zaman aynı formatı izler: Bir ters eğik çizgi (\) karakteriyle başlar, ardından bir ad ve etiketin parametresi gelir. Parametre belirtilmezse, satırın stilindeki varsayılan değer kullanılır.

Bazı etiketler "karmaşıktır" ve birden fazla parametre alır. Bu durumlarda, parametreler parantez içine alınır ve aralarına virgül konur.

**Tipografi üzerine not:**
Bu sayfada, `<` köşeli parantezler içine alınmış ve _italik_ yazılmış her şey bir parametredir ve yerine bir değer girmeniz gerekir. Köşeli parantezler, girmeniz gereken değerin bir parçası değildir. Etiketlerin nasıl girilmesi gerektiği konusunda örnekleri kılavuz olarak kullanın. Genel olarak, tüm etiketlerin görünümü aynı kurallara tabidir.

{{<tag-def-box title="Italics" id="\i">}}
\i1
\i0
{{</tag-def-box>}}
_İtalik_ metni açar veya kapatır. Takip eden metni italik yapmak için `\i1`, italik özelliğini kapatmak için `\i0` kullanın.

{{<tag-def-box title="Bold" id="\b">}}
\b1
\b0
\b<i>\<kalınlık></i>
{{</tag-def-box>}}
**Kalın** metni açar veya kapatır. Takip eden metni kalın yapmak için `\b1`, kalın özelliğini kapatmak için `\b0` kullanın.

<code>\b<i>\<kalınlık></i></code> formu, kullanılacak net bir kalınlık değeri belirtmenize olanak tanır. Çoğu yazı tipinin yalnızca bir veya iki kalınlık desteklediğini ve bu özelliği kullanmanıza nadiren ihtiyaç duyacağınızı unutmayın. Yazı tipi kalınlıkları 100'ün katlarıdır; 100 en düşük, 400 "normal", 700 "kalın" ve 900 en ağır (en kalın) değerdir.

{{<example-box>}}

```ass
I am {\b1}not{\b0} amused.
```

"not" kelimesi kalın yazılır.
{{</example-box>}}

{{<example-box>}}

```ass
{\b100}How {\b300}bold {\b500}can {\b700}you {\b900}get?
```

Kelimeler giderek artan bir kalınlıkla yazılır. Çoğu yazı tipinin bir veya iki farklı kalınlıktan fazlasına sahip olmadığını ve bu durumda sadece "kalın değil" ve "kalın" seçeneklerini görebileceğinizi unutmayın.
{{</example-box>}}

{{<tag-def-box title="Underline" id="\u">}}
\u1
\u0
{{</tag-def-box>}}
<u>Altı çizili</u> metni açar veya kapatır. Takip eden metnin altını çizmek için `\u1`, özelliği kapatmak için `\u0` kullanın.

{{<tag-def-box title="Strikeout" id="\s">}}
\s1
\s0
{{</tag-def-box>}}
<s>Üstü çizili</s> metni açar veya kapatır. Takip eden metnin üstünü çizmek için `\s1`, özelliği kapatmak için `\s0` kullanın.

{{<tag-def-box title="Border size" id="\bord">}}\bord<i>\<boyut></i>{{</tag-def-box>}}
Metin etrafındaki kenarlığın genişliğini değiştirir. Kenarlığı tamamen kaldırmak için boyutu 0 (sıfır) olarak ayarlayın.

"Kenarlık ve gölgeyi ölçekle" (bkz: [betik özellikleri]({{< relref "Properties" >}})) etkinse, değer betik çözünürlüğü pikselleri cinsinden verilir, aksi takdirde video çözünürlüğü pikselleri cinsinden verilir (bu, kenarlık kalınlığının altyazıların oluşturulduğu videonun çözünürlüğüne bağlı olarak değişeceği anlamına gelir).

Değer tam sayı olmak zorunda değildir, ondalık sayı içerebilir. Kenarlık genişliği negatif olamaz.

{{<example-box>}}

```plaintext
\bord0
```

Kenarlığı tamamen devre dışı bırakır.
{{</example-box>}}
{{<example-box>}}

```plaintext
\bord3.7
```

Kenarlık genişliğini 3.7 piksel olarak ayarlar.
{{</example-box>}}

{{<tag-def-box title="Border size (extended)" id="\xbord">}}
\xbord<i>\<boyut></i>
\ybord<i>\<boyut></i>
{{</tag-def-box>}}
Kenarlık boyutunu X ve Y yönlerinde ayrı ayrı ayarlamak için `\xbord` ve `\ybord` etiketlerini kullanın. Bu, anamorfik altyazı oluşturma işlemleri için kenarlık boyutunu düzeltmek adına yararlı olabilir.

Bir satırda `\xbord` veya `\ybord` etiketlerinden sonra `\bord` kullanırsanız, bu etiketin her ikisini de geçersiz kılacağını unutmayın.

Herhangi bir yönde kenarlığı tamamen devre dışı bırakmak için o yöndeki kenarlık genişliğini 0 (sıfır) olarak ayarlayabilirsiniz.

{{<tag-def-box title="Shadow distance" id="\shad">}}\shad<i>\<derinlik></i>{{</tag-def-box>}}
Metinden gölgenin konumlanacağı uzaklığı belirler. Gölgeyi tamamen kaldırmak için derinliği 0 (sıfır) olarak ayarlayın. [\bord]({{< relref "ASS_Tags#\bord" >}}) ile benzer şekilde çalışır.

Gölge uzaklığı bu etiketle negatif olamaz.

{{<tag-def-box title="Shadow distance (extended)" id="\xshad">}}
\xshad<i>\<derinlik></i>
\yshad<i>\<derinlik></i>
{{</tag-def-box>}}
Gölgenin konumlanacağı uzaklığı X ve Y pozisyonları için ayrı ayrı belirler. Gölge, yalnızca hem X hem de Y uzaklığı 0 olduğunda devre dışı bırakılır.

\shad etiketinin aksine, gölgeyi metnin üstüne veya soluna konumlandırmak için bu etiketlerle negatif değerler girebileceğinizi unutmayın.

{{<tag-def-box title="Blur edges" id="\be">}}
\be0
\be1
\be<i>\<güç></i>
{{</tag-def-box>}}
Metin kenarları için ince bir yumuşatma efekti etkinleştirir veya devre dışı bırakır. Efekt her zaman çok görünür değildir, ancak bazı durumlarda metnin daha iyi görünmesini sağlayabilir. Genellikle daha küçük metin boyutlarında daha belirgindir.

Bu etiketin metnin her yerini değil, sadece _kenarlarını_ bulanıklaştırdığını unutmayın. Yani metnin bir kenarlığı varsa ([\bord]({{< relref "ASS_Tags#\bord" >}}) ile ayarlanan), kenarlık bulanıklaşır; ancak kenarlık yoksa, ana metin bulanıklaşır.

Genişletilmiş versiyonda _güç_, normal efektin kaç kez uygulanacağını belirtir. Yüksek değerlerde efektin etkisizleştiğini ve genellikle pek yararlı olmadığını unutmayın. Güçlü bulanıklıklar için `\blur` genellikle daha iyi bir sonuç verir. _Güç_ tam sayı olmalıdır.

{{<tag-def-box title="Blur edges (Gaussian kernel)" id="\blur">}}\blur<i>\<güç></i>{{</tag-def-box>}}
Genel olarak [`\be`]({{< relref "ASS_Tags#\be" >}}) etiketiyle aynı işleve sahiptir, ancak yüksek güç değerlerinde daha iyi görünen daha gelişmiş bir algoritma kullanır. `\be` etiketinden farklı olarak, buradaki _güç_ tam sayı olmayan bir değer olabilir. Efekti devre dışı bırakmak için _gücü_ 0 (sıfır) olarak ayarlayın. Dikkatli olun; _gücü_ çok yüksek ayarlamak, oluşturma (render) sırasında çok fazla işlemci gücü gerektirebilir.

Bu etiketin metnin her yerini değil, sadece _kenarlarını_ bulanıklaştırdığını unutmayın. Yani metnin bir kenarlığı varsa ([\bord]({{< relref "ASS_Tags#\bord" >}}) ile ayarlanan), kenarlık bulanıklaşır; ancak kenarlık yoksa, ana metin bulanıklaşır.

{{<tag-def-box title="Font name" id="\fn">}}\fn<i>\<ad></i>{{</tag-def-box>}}
Takip eden metin için kullanılacak yazı tipini belirler. `\fn` ile yazı tipi adı arasında boşluk olmamalıdır ve yazı tipi adının çevresine parantez veya benzeri işaretler eklememelisiniz.

{{<example-box>}}

```plaintext
\fnArial
```

Bu etiketten sonra gelen metin Arial yazı tipinde olacaktır.
{{</example-box>}}
{{<example-box>}}

```plaintext
\fnTimes New Roman
```

Bu etiketten sonra gelen metin Times New Roman yazı tipinde olacaktır.
{{</example-box>}}

{{<tag-def-box title="Font size" id="\fs">}}\fs<i>\<boyut></i>{{</tag-def-box>}}
Yazı tipi boyutunu ayarlar. Belirtilen boyut, betik pikselleri cinsinden yüksekliktir; yani 40 yazı tipi boyutunda bir metin satırı 40 piksel yüksekliğindedir. (Teknik not: Aslında bu betik pikseli değil, tipografik (masaüstü yayıncılık) punto değeridir ancak oluşturma işlemi her zaman 72 DPI'da (fiili standart gereği) yapıldığı için, bir punto tam olarak bir betik çözünürlüğü pikseline eşit olur.)

Yalnızca tam sayı değerinde yazı tipi boyutları belirleyebilirsiniz.

{{<example-box>}}

```plaintext
\fs10
```

Takip eden metin 10 punto boyutunda bir yazı tipi kullanacaktır.
{{</example-box>}}

{{<tag-def-box title="Font scale" id="\fscx">}}
\fscx<i>\<ölçek></i>
\fscy<i>\<ölçek></i>
{{</tag-def-box>}}
Metnin boyutunu X (`\fscx`) veya Y (`\fscy`) yönünde ayarlar. Belirtilen _ölçek_ yüzde cinsindendir; dolayısıyla 100 "orijinal boyut" anlamına gelir.

Bu, yazı tipi boyutunu ayarlamakla aynı şey değildir; çünkü yazı tipi boyutu ayarı [yazı tipi ipuçlarına](https://en.wikipedia.org/wiki/Font_hinting) (font hinting) tabidir, metni ölçeklendirmek ise ipuçlarından sonra metin şeklini değiştirir. Bu nedenle, yazı tipi ipuçlarındaki değişikliği canlandırmak (animasyon) nadiren istenen bir durum olduğu için, `\fs` yerine her zaman `\t` ile birlikte kullanılmalıdır.

Bu etiketler [vektör çizimlerini]({{< relref "ASS_Tags#drawing-commands" >}}) de etkiler.

Yazı tipi ölçeklendirmesini, anamorfik oluşturmayı düzeltmek ve metin boyutunu [\\fs]({{< relref "ASS_Tags#\fs" >}}) etiketiyle olduğundan daha hassas bir şekilde belirlemek için kullanabilirsiniz.

Eski VSFilter sürümlerinin tam sayı olmayan ölçekleri kırptığını unutmayın.

{{<example-box>}}

```plaintext
\fscx150
```

Metni normalden %50 daha geniş yapar.
{{</example-box>}}
{{<example-box>}}

```plaintext
\fscy50
```

Metni yarım yükseklikte yapar.
{{</example-box>}}
{{<example-box>}}

```plaintext
\fscx200\fscy200
```

Metni iki katına çıkarır.
{{</example-box>}}

{{<tag-def-box title="Letter spacing" id="\fsp">}}\fsp<i>\<aralık></i>{{</tag-def-box>}}
Metindeki harfler arasındaki boşluğu değiştirir. Bunu metni görsel olarak daha fazla yaymak için kullanabilirsiniz. _Aralık_, betik çözünürlüğü pikselleri cinsinden verilir.

Aralık negatif olabilir ve ondalık sayılar içerebilir.

{{<tag-def-box title="Text rotation" id="\frx">}}
\frx<i>\<miktar></i>
\fry<i>\<miktar></i>
\frz<i>\<miktar></i>
\fr<i>\<miktar></i>
{{</tag-def-box>}}
Metni X, Y veya Z ekseni boyunca döndürür. `\fr` etiketi `\frz` etiketi için bir kısayoldur.

- **X ekseni** ekran üzerinde yatay olarak uzanır. Bu eksende döndürme (pozitif değerlerle), metnin üst kısmının ekrandan "içeri" doğru, alt kısmının ise "dışarı" doğru hareket etmesine neden olur.
- **Y ekseni** ekran üzerinde dikey olarak uzanır. Bu eksende döndürme (pozitif değerlerle), metnin sağ tarafının ekrana "girmesine" ve sol tarafının ekrandan "çıkmasına" neden olur.
- **Z ekseni** ekrana diktir. Bu eksende döndürme (pozitif değerlerle), metnin 2D olarak, saat yönünün tersine dönmesine neden olur (derece standartlarına göre).

Döndürme _miktarı_ matematiksel derecelerle ifade edilir; 360 derece tam bir turdur ve 360'ın katlarında döndürme yapmak, döndürme yapmamakla aynıdır. Negatif döndürme miktarlarının yanı sıra 360 dereceden büyük miktarlar belirtmek de mümkündür.

Döndürme işlemi altyazı satırı merkez noktası etrafında gerçekleştirilir; bu, [\\org]({{< relref "ASS_Tags#\org" >}}) etiketi ile tanımlanır.

Bu etiketler [vektör çizimlerini]({{< relref "ASS_Tags#drawing-commands" >}}) de etkiler.

{{<example-box>}}

```plaintext
\frx45
```

Metni X ekseninde 45 derece döndürür.
{{</example-box>}}
{{<example-box>}}

```plaintext
\fry-45
```

Metni Y ekseninde zıt yönde 45 derece döndürür.
{{</example-box>}}
{{<example-box>}}

```plaintext
\frz180
```

Metni Z ekseninde 180 derece döndürerek baş aşağı yapar.
{{</example-box>}}
{{<example-box>}}
Aşağıdaki iki döndürme aynı sonucu verir:

```plaintext
\frz-30
\frz330
```

Çünkü 330 derece, 360 derecelik tam bir turdan 30 derece eksiktir.
{{</example-box>}}
{{<example-box>}}

```plaintext
\t(\frz3600)
```

Metnin Z ekseninde 10 tam tur attığı bir animasyon gerçekleştirin. Ayrıca [\\t]({{< relref "ASS_Tags#\t" >}}) etiketine bakın.
{{</example-box>}}
{{<example-box>}}
Aşağıdaki ekran görüntüleri, farklı eksenlerde döndürme etkisini göstermektedir:

![Fr_örnek01](/img/3.2/Fr_sample01.jpg)

![Fr_örnek02](/img/3.2/Fr_sample02.jpg)

![Fr_örnek03](/img/3.2/Fr_sample03.jpg)
{{</example-box>}}

{{<tag-def-box title="Text shearing" id="\fax">}}
\fax<i>\<faktör></i>
\fay<i>\<faktör></i>
{{</tag-def-box>}}
Metne eğme (perspektif bozulma) dönüşümü uygular. 0 (sıfır) _faktörü_ bozulma olmadığı anlamına gelir.

Genellikle _faktör_ küçük bir sayı olacaktır; -2 ila 2 aralığı dışındaki değerlerin istenen sonuçları vermesi pek olası değildir.

Eğme işlemi döndürmeden sonra, döndürülmüş koordinatlar üzerinde gerçekleştirilir. Eğme için kullanılan koordinat sistemi, [döndürme merkezinden]({{< relref "ASS_Tags#\org" >}}) etkilenmez.

{{<example-box>}}
![eğme](/img/3.2/shearing.png)
{{</example-box>}}

{{<tag-def-box title="Font encoding" id="\fe">}}\fe<i>\<kimlik></i>{{</tag-def-box>}}
Stilin `Kodlama` değerini geçersiz kılar.
Bu nadiren yararlıdır veya iyi bir fikirdir, bu nedenle kaçınılmalıdır.
Daha fazla ayrıntı için [stil belgelerine]({{< relref "Styles#the-style-editor" >}}) bakın.

{{<tag-def-box title="Set color" id="\c">}}
\c&H<i>\<bb>\<gg>\<rr></i>&
\1c&H<i>\<bb>\<gg>\<rr></i>&
\2c&H<i>\<bb>\<gg>\<rr></i>&
\3c&H<i>\<bb>\<gg>\<rr></i>&
\4c&H<i>\<bb>\<gg>\<rr></i>&
{{</tag-def-box>}}
Takip eden metnin rengini belirler. `\c` etiketi `\1c` etiketinin kısaltmasıdır.

- `\1c` birincil dolgu rengini ayarlar.
- `\2c` ikincil dolgu rengini ayarlar. Sadece standart karaoke vurgulamalarında kullanılır.
- `\3c` kenarlık rengini ayarlar.
- `\4c` gölge rengini ayarlar.

Renk kodları, Mavi Yeşil Kırmızı (BGR) sırasıyla [onaltılık](https://en.wikipedia.org/wiki/Hexadecimal) (hexadecimal) olarak verilir. Bunun HTML renk kodlarının tersi olduğuna dikkat edin. Renk kodları her zaman `&H` ile başlamalı ve `&` ile bitmelidir.

Renk Seçici araç çubuğu düğmeleri ![renk-seçici-araç-çubuğu-düğmeleri](/img/3.2/pick-color-toolbar-buttons.png), renkleri seçmenize ve renk kodlarını girmenize yardımcı olabilir.

{{<tag-def-box title="Set alpha" id="\alpha">}}
\alpha&H<i>\<aa></i>
\1a&H<i>\<aa></i>
\2a&H<i>\<aa></i>
\3a&H<i>\<aa></i>
\4a&H<i>\<aa></i>
{{</tag-def-box>}}
Metnin alfa (saydamlık) değerini ayarlar.

- `\alpha` tüm bileşenlerin alfasını aynı anda ayarlar.
- `\1a` birincil dolgu alfasını ayarlar.
- `\2a` ikincil dolgu alfasını ayarlar. Sadece standart karaoke vurgulamalarında kullanılır.
- `\3a` kenarlık alfasını ayarlar.
- `\4a` gölge alfasını ayarlar.

00 (sıfır) alfası tamamen opak/görünür, FF (yani onluk sistemde 255) alfası ise tamamen saydam/görünmez anlamına gelir.

{{<example-box>}}

```plaintext
\alpha&H80&
```

Tüm bileşenlerin alfasını onaltılık 80, onluk sistemde 128 olarak ayarlayarak metni genel olarak %50 saydam yapar.
{{</example-box>}}
{{<example-box>}}

```plaintext
\1a&HFF&
```

Birincil dolgu alfasını onaltılık FF, onluk sistemde 255 olarak ayarlar, metni görünmez kılar ve geriye sadece kenarlık ve gölge kalır.
{{</example-box>}}

{{<tag-def-box title="Line alignment" id="\an">}}\an<i>\<konum></i>{{</tag-def-box>}}
Satırın hizalamasını belirler. Hizalama, herhangi bir [pozisyon geçersiz kılma]({{< relref "ASS_Tags#\pos" >}}) veya [hareket]({{< relref "ASS_Tags#\move" >}}) devrede olmadığında satırın konumunu belirler, aksi takdirde konumlandırma ve döndürme için çapa noktası (anchor point) işlevi görür.

`\an` etiketi, _konum_ için "sayısal tuş takımı" değerlerini kullanır; yani hizalama değerleri, standart bir klavyedeki sayısal tuş takımındaki basamakların konumlarına karşılık gelir:

1. Sol alt
2. Orta alt
3. Sağ alt
4. Sol orta
5. Orta merkez
6. Sağ orta
7. Sol üst
8. Orta üst
9. Sağ üst

{{<tag-def-box title="Line alignment (legacy)" id="\a">}}\a<i>\<konum></i>{{</tag-def-box>}}
SubStation Alpha'dan miras kalan hizalama kodlarını kullanarak satırın hizalamasını belirler. Bu etiket desteklenir ancak artık kullanılmamaktadır; daha sezgisel olduğu için yeni betiklerde genellikle `\an` kullanmalısınız.

İstisna olarak, hızlı çeviri yapanlar için `\a6` kullanılabilir, çünkü tembellik edecekseniz bunu düzgün yapıp fazladan karakterden tasarruf etmelisiniz.

_Konum_ değerini şu şekilde hesaplayın: Sola hizalama için 1, merkeze hizalama için 2 ve sağa hizalama için 3 kullanın. Altyazılar için işlem tamamdır. Üst altyazılar için sayıya 4 ekleyin, orta altyazılar için sayıya 8 ekleyin:

- 1: Sol alt
- 2: Orta alt
- 3: Sağ alt
- 5: Sol üst
- 6: Orta üst
- 7: Sağ üst
- 9: Sol orta
- 10: Orta merkez
- 11: Sağ orta

{{<tag-def-box title="Karaoke effect" id="\k">}}
\k<i>\<süre></i>
\K<i>\<süre></i>
\kf<i>\<süre></i>
\ko<i>\<süre></i>
\kt<i>\<zaman></i>
{{</tag-def-box>}}

> _Lütfen bu etiketlerin tek başlarına sadece çok belirli efektler yarattığını ve diğer tüm efektlerin birden fazla farklı etiketin birleşimiyle oluşturulduğunu unutmayın._

`\k` etiket ailesi, her hecenin süresini belirleyerek karaoke efektleri için altyazıları işaretler. Satırdaki her heceden önce bir `\k` etiketi yerleştirirsiniz.

_Süre_, santisaniye cinsinden verilir; yani 100'lük bir _süre_ 1 saniyeye eşittir. `\k` etiketlerini genellikle manuel olarak girmezsiniz, [Aegisub karaoke modu]({{< relref "Tutorials#karaoke-timing" >}}) gibi karaoke zamanlama araçlarını kullanırsınız.

Farklı `\k` etiketleri çeşitli efektler yaratır:

- `\k`: Vurgulamadan önce, hece ikincil renk ve alfa ile doldurulur. Hece başladığında, dolgu anında birincil renk ve alfaya geçer.
- `\K` ve `\kf`: Bu ikisi özdeştir. `\K`'nin büyük harf K olduğunu ve küçük harf `\k`'den farklı olduğunu unutmayın. Hece dolgusu ikincil renkle başlar; hece başladığında, dolgu soldan sağa doğru bir tarama ile ikincilden birincile geçer, böylece tarama hece süresi bittiğinde sona erer.
- `\ko`: `\k` benzeridir, ancak vurgulamadan önce hecenin kenarlığı/anahatları kaldırılır ve hece başladığında anında belirir.

> _Not: `\kt` etiketi henüz tüm Aegisub içi araçlar tarafından desteklenmemektedir ve harici betikler de onu düzgün şekilde işlemeyebilir._

Ayrıca `\kt` etiketi, sonraki karaoke hecesinin başlangıç zamanını olayın başlangıcına göre ayarlar. `\kt` olmadan, her hece başlangıcı dolaylı olarak önceki tüm hecelerin süresinin toplamı olarak belirlenir.

{{<tag-def-box title="Wrap style" id="\q">}}\q<i>\<stil></i>{{</tag-def-box>}}
Satır sonlarının altyazı satırına nasıl uygulanacağını belirler. Şu _stil_ değerleri mevcuttur:

- 0: Akıllı kaydırma, her satırı yaklaşık olarak eşit uzunlukta yapar, ancak eşit uzunluk mümkün olmadığında üst satırı daha geniş tutar. Sadece `\N` satır sonlarını zorlar.
- 1: Satır sonu kaydırma, bir satıra mümkün olduğunca fazla metin doldurur, ardından bir sonraki satıra geçer. Sadece `\N` satır sonlarını zorlar.
- 2: Sözcük kaydırma yok, geniş satırlar ekranın kenarlarının ötesine uzanır. Hem `\n` hem de `\N` satır sonlarını zorlar.
- 3: Akıllı kaydırma, stil 0'a benzer, ancak alt satırlar daha geniş yapılır.

{{<tag-def-box title="Reset style" id="\r">}}\r<br>\r<i>\<stil></i>{{</tag-def-box>}}
Stili sıfırlar. Bu, [animasyonlar]({{< relref "ASS_Tags#\t" >}}) dahil olmak üzere, takip eden tüm metinler için geçerli olan tüm stil geçersiz kılmalarını iptal eder.

_Stil_ belirtilmeyen ilk form, tüm satır için tanımlanmış stile geri dönerken; bir _stil_ adı belirten ikinci form, stili o belirli stile sıfırlar.

{{<example-box>}}

```ass
-Hey\N{\rAlternate}-Huh?\N{\r}-Who are you?
```

Mevcut satır stilinin "Default" olduğunu varsayarsak, ilk "Hey" Default stilinde olur, sonraki satırda "Huh?" "Alternate" stilinde devam eder ve üçüncü satırda stil "Who are you?" metni için "Default"a sıfırlanır.
{{</example-box>}}

{{<tag-def-box title="Set position" id="\pos">}}\pos(<i>\<X></i>,<i>\<Y></i>){{</tag-def-box>}}
Satırın konumunu belirler. _X_ ve _Y_ koordinatları tam sayı olmalı ve betik çözünürlüğü koordinat sisteminde verilmelidir. _X_ ve _Y_'nin anlamı [hizalamaya]({{< relref "ASS_Tags#\an" >}}) bağlı olarak biraz değişir.

Altyazı satırının hizalaması, konum için çapa noktası olarak kullanılır. Yani, sola üstten hizalı bir satırınız olduğunda, altyazının sol üst köşesi `\pos` ile verilen koordinatlara yerleştirilir; alt-merkez hizalaması için ise altyazının alt orta noktası belirtilen koordinatlara yerleştirilir.

{{<example-box>}}
Aşağıdaki ekran görüntüleri, hizalamanın konumlandırmayı nasıl etkilediğini göstermektedir.
Yeşil çarpı işareti, videodaki (320,240) noktasını işaretler.

![Pos_örnek01](/img/3.2/Pos_sample01.jpg)
![Pos_örnek02](/img/3.2/Pos_sample02.jpg)
![Pos_örnek03](/img/3.2/Pos_sample03.jpg)
{{</example-box>}}

{{<tag-def-box title="Movement" id="\move">}}
\move(<i>\<x1</i>>,<i>\<y1</i>>,<i>\<x2</i>>,<i>\<y2</i>>)
\move(<i>\<x1</i>>,<i>\<y1</i>>,<i>\<x2</i>>,<i>\<y2</i>>,<i>\<t1</i>>,<i>\<t2</i>>)
{{</tag-def-box>}}
`\move` etiketi, altyazı satırını konumlandırması açısından [`\pos`]({{< relref "ASS_Tags#\pos" >}}) etiketine benzer şekilde çalışır; farkı, `\move` etiketinin altyazıyı hareket ettirmesidir.

`\move` etiketinin iki versiyonu arasındaki fark, birinin hareketi altyazının tüm süresi boyunca gerçekleştirmesi, diğerinde ise hareketin gerçekleşeceği süreyi belirtmenizdir.

_x1_, _y1_, _x2_ ve _y2_ koordinatları, `\pos` gibi betik çözünürlüğü koordinat sisteminde verilir. Altyazı (x1, y1) noktasında başlar ve sabit hızla hareket ederek (x2, y2) noktasında biter. [Hizalama]({{< relref "ASS_Tags#\an" >}}), hareket koordinatlarını `\pos` koordinatlarını etkilediği gibi etkiler.

İkinci versiyonda, _t1_ ve _t2_ süreleri milisaniye (saniyenin binde biri) cinsinden verilir ve altyazının başlangıç zamanına göredir. Örneğin, 1500'lük bir _t1_ değeri, hareketin satır ekranda belirdikten 1.5 saniye sonra başladığı anlamına gelir. Hareket için süreleri belirttiğinizde, altyazının konumu şu şekilde olur:

1. _t1_'den önce altyazı (x1, y1) noktasında sabittir.
2. _t1_ ile _t2_ arasında, altyazı (x1, y1)'den (x2, y2)'ye sabit hızla hareket eder.
3. _t2_'den sonra altyazı (x2, y2) noktasında sabittir.

_t1_ ve _t2_ değerlerini satırın süresinden daha büyük belirtmenin yasal olduğunu, ancak bunun pek yararlı olmayabileceğini unutmayın. _t1_ ve _t2_ değerlerinin her ikisini de 0 (sıfır) olarak belirtmek, `\move` etiketinin ilk versiyonunu kullanmakla aynıdır; yani hareket, satırın başlangıç zamanından bitiş zamanına kadar gerçekleşir.

**`\move` etiketinin yapamayacağı bazı şeyler vardır**:

- Sabit olmayan hızda hareket mümkün değildir. Hareket, örneğin yavaş başlayıp hızlı bitemez.
- Bir satırda yalnızca bir konumlandırma veya hareket etiketi olabilir. Bir satıra hem `\pos` hem de `\move` etiketi koymak çalışmaz. Bir satıra iki veya daha fazla `\move` etiketi koymak da çalışmaz.

Bunlardan herhangi birini yapmanız gerekirse, hareketi ayrı altyazı satırlarında gerçekleştirilen bölümlere ayırmanız gerekir. (Bunun nasıl yapılacağı bu sayfanın kapsamı dışındadır.)

{{<example-box>}}

```plaintext
\move(100,150,300,350)
```

Satır ekranda belirdiğinde, altyazı (100,150) noktasındadır. Altyazı görüntülendiği sürece, kaybolduğu anda (300,350) noktasına varacak şekilde sabit hızla hareket eder.
{{</example-box>}}
{{<example-box>}}

```plaintext
\move(100,150,300,350,500,1500)
```

Satır (100,150) noktasında belirdi. Satır yarım saniye (500 milisaniye) görüntülendikten sonra, satırın ilk belirdiği andan itibaren bir buçuk saniye (1500 milisaniye) sonra noktaya varacak şekilde (300,350) noktasına doğru hareket etmeye başlar.
{{</example-box>}}

{{<tag-def-box title="Rotation origin" id="\org">}}\org(<i>\<X></i>,<i>\<Y></i>){{</tag-def-box>}}
[Döndürme]({{< relref "ASS_Tags#\frx" >}}) için kullanılan merkez noktasını ayarlar. Bu, satırın tüm döndürmelerini etkiler. _X_ ve _Y_ koordinatları tam sayı betik çözünürlüğü pikselleri cinsinden verilir.

Bir satırda `\org` etiketi olmadığında, döndürme merkezi dolaylı olarak [konum çapa noktası]({{< relref "ASS_Tags#\pos" >}}) ile aynıdır. Bu, satır hareket ederse ve `\org` ile ayarlanmış bir merkez yoksa döndürme merkezinin de hareket edeceği anlamına gelir. `\org` etiketine animasyon uygulayamayacağınızı, kullanırsanız sabit bir merkezle sınırlı kalacağınızı unutmayın.

Döndürme merkezi 3D bir sahnedeki kaçış noktasına yerleştirilirse, altyazı satırının 3D döndürmeleri sahneyle eşleşecek doğru perspektifi üretecektir.

Merkez noktasını gerçek görüntünün çok dışına yerleştirmek kesinlikle mümkündür (ve bazen yararlıdır); yeterince uzak bir noktaya yerleştirilirse, hesaplanmış küçük döndürmeler yapmak metni görüntü boyunca düz (veya neredeyse düz) bir çizgi üzerinde hareket ettiriyormuş gibi görünecektir. Bunu kontrol etmek biraz zordur, ancak `\move` ile ilgili format sınırlamalarını (örneğin hızlanan hareket yapamamak veya satır başına birden fazla hareket yapamamak gibi) aşmak için kullanılabilir.

Bir satırda en fazla bir `\org` etiketi olabilir; bir satıra birden fazla koyarsanız sadece ilki kullanılır.

{{<example-box>}}

```plaintext
\org(320,240)
```

Döndürme merkezini (320,240) noktasına sabitler.
{{</example-box>}}
{{<example-box>}}

```plaintext
\org(10000,0)
```

Döndürme merkezini uzak bir noktaya yerleştirmek, "sıçrama" efektleri üretmek için hafif `\frz` döndürmeleri kullanmanıza olanak tanır; metin döndürülüyormuş gibi görünmeden yukarı veya aşağı hareket edecektir.
{{</example-box>}}

{{<tag-def-box title="Fade" id="\fad">}}\fad(<i>\<fadein></i>,<i>\<fadeout></i>){{</tag-def-box>}}
Bir kararma (fade-in) ve aydınlanma (fade-out) efekti oluşturur. _Fadein_ ve _fadeout_ süreleri milisaniye cinsinden verilir; yani 1000, bir saniye demektir. Bu uçlarda herhangi bir efekt olmaması için _fadein_ veya _fadeout_ değerini 0 (sıfır) olarak belirleyebilirsiniz.

Efekt eklemek satırın süresini uzatmaz, aksine satırın görüntülenme süresinin başı veya sonu efekt için kullanılır. Bu nedenle, _fadein_ + _fadeout_ değerinin satırın süresinden büyük olmamasına dikkat etmelisiniz. Örneğin, 4 saniye görüntülenen bir satır için _fadein_ + _fadeout_ toplamı 4000'den büyük olmamalıdır.

{{<example-box>}}

```plaintext
\fad(1200,250)
```

Satırı görüntülendiği ilk 1.2 saniye boyunca karartın ve görüntülendiği son çeyrek saniye boyunca aydınlatın.
{{</example-box>}}

{{<tag-def-box title="Fade (complex)" id="\fade">}}\fade(<i>\<a1</i>>,<i>\<a2</i>>,<i>\<a3</i>>,<i>\<t1</i>>,<i>\<t2</i>>,<i>\<t3</i>>,<i>\<t4</i>>){{</tag-def-box>}}
Üç alfa değeri (_a1_, _a2_ ve _a3_) ve dört zaman (_t1_, _t2_, _t3_ ve _t4_) kullanarak beş bölümlü bir geçiş gerçekleştirin.

Alfa değerleri _onluk sistemde_ verilir ve 0 ile 255 arasındadır; 0 tamamen görünür, 255 ise görünmezdir. Zaman değerleri, satırın başlangıcından itibaren milisaniye cinsinden verilir. Yedi parametrenin tamamı gereklidir. (En yaygın geçiş efektleri için [`\fad`]({{< relref "ASS_Tags#\fad" >}}) etiketi gayet iyi çalışır.)

- _t1_'den önce, satır _a1_ alfasına sahiptir.
- _t1_ ile _t2_ arasında, satır _a1_ alfasından _a2_ alfasına geçer.
- _t2_ ile _t3_ arasında, satır sabit olarak _a2_ alfasına sahiptir.
- _t3_ ile _t4_ arasında, satır _a2_ alfasından _a3_ alfasına geçer.
- _t4_'ten sonra, satır _a3_ alfasına sahiptir.

{{<example-box>}}

```plaintext
\fade(255,32,224,0,500,2000,2200)
```

Görünmez başlar, neredeyse tamamen opak hale gelir, ardından neredeyse tamamen görünmez olur. İlk geçiş satır başladığında başlar ve 500 milisaniye sürer. İkinci geçiş 1500 milisaniye sonra başlar ve 200 milisaniye sürer.
{{</example-box>}}

{{<tag-def-box title="Animated transform" id="\t">}}
\t(<i>\<stil değiştiriciler></i>)
\t(<i>\<hızlanma></i>,<i>\<stil değiştiriciler></i>)
\t(<i>\<t1</i>>,<i>\<t2</i>>,<i>\<stil değiştiriciler></i>)
\t(<i>\<t1</i>>,<i>\<t2</i>>,<i>\<hızlanma></i>,<i>\<stil değiştiriciler></i>)
{{</tag-def-box>}}

Bir stilden diğerine kademeli, animasyonlu bir geçiş gerçekleştirin. _Stil değiştiriciler_, bu referansta belirtilen diğer geçersiz kılma etiketleridir. Geçersiz kılma etiketlerinin yalnızca sınırlı bir seti `\t` ile canlandırılabilir:

| Yazı Tipi | Geometri | Diğer efektler |
| --------- | -------- | -------------- |
| \\fs      | \\fscx   | \\bord         |
| \\fsp     | \\fscy   | \\xbord        |
| \\c       | \\frx    | \\ybord        |
| \\1c      | \\fry    | \\shad         |
| \\2c      | \\frz    | \\xshad        |
| \\3c      | \\fr     | \\yshad        |
| \\4c      | \\fax    | \\clip         |
| \\alpha   | \\fay    | \\iclip        |
| \\1a      |          | \\be           |
| \\2a      |          | \\blur         |
| \\3a      |          |                |
| \\4a      |          |                |

_Not: `\clip` ve `\iclip` için sadece dikdörtgen versiyonlar canlandırılabilir. Vektör çizimi versiyonları canlandırılamaz._

_Not: `\t` etiketlerinde `\clip` ve `\iclip` karıştırmak istenmeyen sonuçlar doğurur._

_t1_ ve _t2_ parametreleri, dönüşümün gerçekleştirileceği zaman aralığını belirtir. _t1_ ve _t2_ olmayan versiyonlarda, dönüşüm satırın tüm süresi boyunca gerçekleştirilir. Süreler milisaniye cinsinden verilir ve satırın başlangıç zamanına göredir. (Açıklamanın geri kalanı için, _t1_ ve _t2_'nin belirtildiği veya dolaylı olarak 0 ile satır süresi olduğu varsayılır.)

_Hızlanma_ parametresi, animasyonu doğrusal olmayan hale getirmek ve bunun yerine üstel bir eğriyi takip etmesini sağlamak için kullanılabilir. 1 (bir) _hızlanma_ parametresi, animasyon hızının doğrusal olmasına neden olur. 0 ile 1 arasındaki bir değer, animasyonun hızlı başlayıp yavaş bitmesine neden olur. 1'den büyük bir değer, animasyonun yavaş başlayıp hızlı bitmesine neden olur. (Matematiksel olarak eğilimli olanlar için fonksiyon: _y_ = _x_ üzeri _hızlanma_, _x_ ∈ [0;1] = (_t_-_t1_)/(_t2_-_t1_), _t_ mevcut zamandır.)

_t1_'den önce stil, `\t` etiketinden önceki tüm etiketlerin belirttiği gibidir. _t2_'den sonra stil, `\t` etiketinden önceki tüm etiketlerin belirttiği gibi ve verilen _stil geçersiz kılmaları_ ile daha da geçersiz kılınmış haldedir. _t1_ ile _t2_ arasında stil, yukarıda açıklanan hızlanma fonksiyonunu takip ederek bu iki nokta arasında kademeli olarak canlandırılır.

{{<example-box>}}

```ass
{\1c&HFF0000&\t(\1c&H0000FF&)}Hello!
```

Metin mavi başlar, ancak kırmızıya doğru solar, böylece satır bittiğinde tamamen kırmızı olur.
{{</example-box>}}
{{<example-box>}}

```ass
{\an5\t(0,5000,\frz3600)}Wheee
```

Metnin 5 saniye boyunca saat yönünün tersine 10 kez dönmesini sağlar.
{{</example-box>}}
{{<example-box>}}

```ass
{\an5\t(0,5000,0.5,\frz3600)}Wheee
```

Yukarıdakinin aynısıdır, ancak 5 saniyede 10 turu tamamlayarak hızlı başlayıp yavaşlayacaktır.
{{</example-box>}}
{{<example-box>}}

```ass
{\an5\fscx0\fscy0\t(0,500,\fscx100\fscy100)}Boo!
```

Metin sıfır boyutta, yani görünmez başlar, ardından X ve Y yönünde %100 boyuta büyür.
{{</example-box>}}

{{<tag-def-box title="Clip (rectangle)" id="\clip">}}
\clip(<i>\<x1</i>>,<i>\<y1</i>>,<i>\<x2</i>>,<i>\<y2</i>>)
\iclip(<i>\<x1</i>>,<i>\<y1</i>>,<i>\<x2</i>>,<i>\<y2</i>>)
{{</tag-def-box>}}
Satırı kırpmak (clip) için bir dikdörtgen tanımlayın; satırın yalnızca dikdörtgenin içindeki kısmı görünür. `\iclip` etiketi tam tersi etkiye sahiptir, satırın gösterilmediği bir dikdörtgen tanımlar.

_x1_, _y1_, _x2_ ve _y2_ koordinatları betik çözünürlüğü pikselleri cinsinden verilir ve videonun sol üst köşesine göredir. Koordinatlar tam sayı olmalıdır, tam sayı olmayan koordinat kullanma imkanı yoktur. (Betik çözünürlüğünü artırmak hassasiyeti artırmaz, kırpma her zaman video piksel sınırlarında gerçekleşir.)

{{<example-box>}}

```plaintext
\clip(0,0,320,240)
```

640x480 betik çözünürlüğü varsayıldığında, satırın yalnızca sol üst kadran içindeki kısmı görünür.
{{</example-box>}}
{{<example-box>}}

```plaintext
\iclip(0,0,320,240)
```

Yukarıdakine benzer, ancak bunun yerine sol üst kadrandaki satır kısmı gizlenir.
{{</example-box>}}
{{<example-box>}}
704x480 videoda `\clip(0,0,704,245)` örneği:

![Clip_örnek01](/img/3.2/Clip_sample01.jpg)
{{</example-box>}}

{{<tag-def-box title="Clip (vector drawing)" id="">}}
\clip(<i>\<çizim komutları></i>)
\clip(<i>\<ölçek></i>,<i>\<çizim komutları></i>)
\iclip(<i>\<çizim komutları></i>)
\iclip(<i>\<ölçek></i>,<i>\<çizim komutları></i>)
{{</tag-def-box>}}
Satırın kısımlarını seçerek görüntülemek (`\clip`) veya gizlemek (`\iclip`) için bir vektör çizimi tarafından tanımlanan şekli kullanın.

_Çizim komutları_, `\p` etiketi ile kullanılanlarla aynıdır; koordinatlar betik çözünürlüğü pikselleri cinsinden verilir ve videonun sol üst köşesine göredir.

_Ölçek_ belirtilmemişse 1 (bir) olduğu varsayılır; bu, koordinatların doğrudan piksellere karşılık geldiği anlamına gelir. _Ölçek_, `\p` çizimleri için kullanılan _ölçek_ ile aynı şekilde çalışır.

Dikdörtgen kırpmanın aksine, vektör çizimi kırpma `\t` ile canlandırılamaz. Bir vektör çizimi kırpmasını canlandırmanız gerekirse, kırpma animasyonunun her "kare"si için ayrı benzer altyazı satırları oluşturmanız gerekir.

{{<example-box>}}

```plaintext
\clip(1,m 50 0 b 100 0 100 100 50 100 b 0 100 0 0 50 0)
```

Satırın yalnızca tanımlanan sözde daire içindeki kısmını gösterir.
{{</example-box>}}

## Çizim etiketleri

Advanced Substation Alpha, vektörel grafiklerle çizim yapmanıza olanak tanıyan bazı gelişmiş çizim etiketlerini de destekler. Vektörlere ve eğrilere (splines) aşinalık, bunu anlamayı çok daha kolaylaştıracaktır.

### \p\<0/1/..> - Çizim modunu aç/kapat

Bu etiketi 1 veya daha yüksek bir değere ayarlamak, çizim modunu etkinleştirir. Bu geçersiz kılma bloğundan sonraki metin, görsel metin olarak değil, çizim talimatları olarak yorumlanır. Bunu sıfıra ayarlamak çizim modunu devre dışı bırakır ve normal davranışı geri yükler. Açarken, değer sıfırdan büyük herhangi bir tam sayı olabilir ve 2^(değer-1) modunda ölçek olarak yorumlanır. Bu, alt-piksel hassasiyetine izin vermek için yapılır.
örneğin:

```plaintext
\p1
```

(Normal koordinatlarla çizimi etkinleştirir)

```plaintext
\p0
```

(Çizimi devre dışı bırakır)

```plaintext
\p2
```

(Çizimi etkinleştirir ve çözünürlük iki katına çıkar. Yani 200,200'e çizim yapmak aslında 100,100'e çizim yapar)

```plaintext
\p4
```

(Çizimi etkinleştirir ve çözünürlük 8 kat daha büyüktür (2^(4-1)). Yani 400,400'e çizim yapmak aslında 50,50'ye çizim yapar)

### \pbo\<y> - Temel çizgi ofseti

Çizim için temel çizgi ofsetini tanımlar. Bu temelde tüm koordinatlar için bir Y ofsetidir.
örneğin:

```plaintext
\pbo-50
```

(Her şeyi belirtilenin 50 piksel yukarısına çizer)

```plaintext
\pbo100
```

(Her şeyi belirtilenin 100 piksel aşağısına çizer)

## Çizim komutları

Bu komutlar bir \clip etiketi (vektörel aşırı yükleme) içinde veya \p# ile \p0 arasında, geçersiz kılma bloklarının dışında yer almalıdır. Örneğin (doğrudan ASS teknik özelliklerinden alınmıştır):

- Kare:

  ```ass
  {\p1}m 0 0 l 100 0 100 100 0 100{\p0}
  ```

- Yuvarlatılmış kare:

  ```ass
  {\p1}m 0 0 s 100 0 100 100 0 100 c{\p0}
  ```

  (c bu durumda "p 0 0 100 0 100 100"e eşittir)

- Daire (neredeyse):

  ```ass
  {\p1}m 50 0 b 100 0 100 100 50 100 b 0 100 0 0 50 0{\p0}
  ```

  (2. 'b'nin burada isteğe bağlı olduğuna dikkat edin)

Çizim komutları, dolgu için birincil rengi ve kenarlıklar için anahat rengini kullanır. Ayrıca gölgeyi görüntülerler. Vektör çizme fikri şudur: Video karesinde görünmez bir "imleç" (bunu bir çizim programındaki fare işaretçisi veya görüntü boyunca hareket eden bir kalem olarak düşünün) vardır ve ona başka konumlara hareket etmesini söylersiniz. Hareket ederken arkasındaki alana çizer ve oluşturduğu çizgiyi kapattığınızda, orayı birincil renkle doldurur.

### m \<x> \<y> - Taşı

İmleci x,y konumuna taşır. Kapatılmamış bir şekliniz varsa, program yeni, bağımsız bir şekil çizdiğinizi varsaydığı için otomatik olarak kapatılacaktır. Tüm çizim rutinleri bu komutla başlamalıdır.

### n \<x> \<y> - Taşı (kapatmadan)

İmleci mevcut şekli kapatmadan x,y konumuna taşır.

### l \<x> \<y> - Çizgi

Mevcut imleç konumundan x,y konumuna bir çizgi çizer ve ardından imleci oraya taşır.

### b \<x1> \<y1> \<x2> \<y2> \<x3> \<y3> - Kübik Bézier eğrisi

(x1,y1) ve (x2,y2) noktalarını kontrol noktaları olarak kullanarak, imleç konumundan (x3,y3) konumuna kübik (3. derece) bir Bézier eğrisi çizer. Bézier eğrileri hakkında daha fazla bilgi için [Wikipedia'daki makaleye](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) göz atın. Bu makaleden alınan resimde, P0 imleç konumu, P1 x1,y1, P2 x2,y2 ve P3 x3,y3'tür:

![Bézier](/img/3.2/Bezier.png)

Eğrinin P0'da başladığını, P1'e doğru ilerlediğini, ardından P2'nin yönünden gelerek P3'e ulaştığını unutmayın.

### s \<x1> \<y1> \<x2> \<y2> \<x3> \<y3> .. \<xN> \<yN> - Kübik b-spline

N noktasına kadar kübik (3. derece) bir düzgün b-spline çizer. Bu en az 3 koordinat içermelidir (bu durumda b ile aynıdır). Bu temelde birkaç kübik Bézier eğrisini birbirine bağlamanıza olanak tanır. Daha fazla bilgi için Wikipedia'daki diğer makaleye göz atın.

### p \<x> \<y> - b-spline'ı genişlet

b-spline'ı x,y konumuna genişletir. Bu, esasen s'nin sonuna başka bir koordinat çifti eklemekle aynıdır.

### c - b-spline'ı kapat

b-spline'ı kapatır.

_Not: [Vektör kırpma görsel dizgi aracı]({{< relref "Visual_Typesetting#vectorial-clip" >}}) yalnızca m, l ve b komutlarını destekler ve diğer komutları kullanan çizimleri bozabilir._