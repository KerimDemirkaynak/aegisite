---
title: Altyazı Düzenleme
menu:
  docs:
    parent: working-with-subtitles
weight: 3000
aliases:
  - /docs/latest/Editing_Subtitles/
---

Altyazı düzenleme, Aegisub'ın temel varoluş amacıdır. Bu sayfa, altyazı satırlarının temel metin düzenleme işlemleriyle ilgilidir; altyazı tipografisi hakkında daha fazla bilgi için [dizgi (typesetting)]({{< relref "Typesetting" >}}) bölümüne bakın. Altyazı satırlarının zamanlaması hakkında bilgi için [ses ile çalışma]({{< relref "Audio" >}}) bölümüne bakın.

## Altyazı açma

_Dosya_ menüsünde, altyazı açma veya oluşturma ile ilgili dört seçenek bulunur:

Yeni altyazılar
: Yeni, boş bir betik oluşturur (mevcut dosyayı kapatır).

Altyazıları aç
: Mevcut bir altyazı dosyasını açar veya bir [Matroska kapsayıcı dosyasından](https://www.matroska.org) altyazı içe aktarır.

Altyazıları karakter kodlamasıyla aç
: Altyazıları açar ancak Aegisub'ın dosyayı yorumlamak için kullanacağı karakter kümesini seçmenize olanak tanır. Genellikle gerekli değildir, ancak alışılmadık bir karakter kümesine sahip bir dosyanız varsa, Aegisub bazen dosyayı yanlış algılayabilir.

Videodan altyazıları aç
: Şu anda açık olan video dosyasına gömülü altyazıları açar. Bu özellik şu an sadece Matroska video dosyalarıyla çalışmaktadır.

[Otomatik Kaydedilen Altyazıları]({{< relref "Autosave" >}}) aç
: Aegisub'ın otomatik kaydetme özelliği tarafından oluşturulan bir dosyayı açar. Aegisub, kaydedilmemiş değişiklikleriniz varken çökerse veya sadece dosyanın daha eski bir sürümünü açmak isterseniz kullanışlıdır.

Unicode olarak algılanmayan bir altyazı dosyası açtığınızda, Aegisub dosyanın hangi karakter kümesiyle kodlandığını tahmin etmeye çalışır. Eğer emin olamazsa, iki veya daha fazla olası alternatif arasından seçim yapmanızı ister. Sonuç bozuk veya hatalı görünüyorsa, dosyayı başka bir karakter kümesiyle tekrar açmayı deneyin.

### Desteklenen formatlar

Aegisub, aşağıdaki altyazı formatlarını okumayı destekler:

- Advanced Substation Alpha, diğer adıyla SSA v4+ (.ass)
- Substation Alpha v4 (.ssa)
- [SubRip](https://zuggy.wz.cz/) Metin (.srt)
- MPEG4 Zamanlı Metin (en iyi ihtimalle sınırlı destek; en kötü ihtimalle bozuk), diğer adıyla ISO/IEC 14496-17, MPEG-4 Bölüm 17 veya sadece TTXT (.ttxt)
- MicroDVD (.sub)
- Düz "diyalog betiği" formatlı metin (aşağıya bakın)

### MKV'den altyazı içe aktarma

Altyazıları doğrudan Matroska dosyalarından yüklemek de mümkündür. Aşağıdaki CodecID'ler desteklenir:

- S_TEXT/UTF8 (SRT)
- S_TEXT/ASS (ASS/SSA v4+)
- S_TEXT/SSA (SSA v4)

### Düz metin betiklerini içe aktarma

Aegisub, "diyalog formatlı" düz metin betiklerinin içe aktarılmasını da destekler. Örneğin:

```plaintext
Oyuncu 1: Konuşmanı anlıyorum, yine de pek az yabancı anlar.
         Öyleyse neden Ortak Dilde konuşmuyorsun,
         Batı'da adet olduğu üzere, eğer cevap almayı istiyorsan?
# TL kontrol: Yukarıdaki metin Yüzüklerin Efendisi'nden bir alıntı gibi görünüyor, daha sonra kontrol et
Oyuncu 2: Nelerden bahsediyorsun sen?
```

Bu işlem, biri yorum satırı olmak üzere beş altyazı satırı ile sonuçlanacaktır. İlk üç satırın oyuncu alanı "Oyuncu 1" olarak, beşinci satır ise "Oyuncu 2" olarak ayarlanacaktır (yorum satırının oyuncu alanı boş kalacaktır).

.txt uzantılı bir dosya açtığınızda, Aegisub sizden oyuncu ayırıcı ve yorum başlatıcı olarak hangi karakterleri kullanması gerektiğini soracaktır. Yukarıdaki örnekte, oyuncu ayırıcı iki nokta üst üste ("`:`") ve yorum başlatıcı diyez işaretidir ("`#`").

## Altyazıları düzenleme

Aegisub'da altyazı düzenleme iki alanda yapılır: altyazı düzenleme kutusu (metni yazdığınız veya düzenlediğiniz yer) ve altyazı ızgarası. Hem düzenleme kutusunda hem de ızgarada yapılan değişiklikler normalde sadece düzenleme kutusunda görüntülenen satırı değil, seçili olan tüm satırları etkiler.

### Altyazı düzenleme kutusu

![altyazı_düzenleme_kutusu](/img/3.2/subs_edit_box.png)

Düzenleme kutusu, bir dizi ilişkili kontrol düğmesiyle birlikte gelen düz bir metin düzenleme alanıdır. Bunlar:

1. Satırı yorum olarak işaretler. Yorum satırları videoda görüntülenmez.
1. Bu satır için kullanılan [stil]({{< relref "Styles" >}}).
1. Bu satırı konuşan oyuncu. Altyazı gösteriminde gerçek bir etkisi yoktur ancak düzenleme amaçları için kullanışlı olabilir.
1. Bu satır için efekt. Bu alan aracılığıyla uygulanabilen birkaç önceden tanımlanmış efekt vardır, ancak oluşturucunun (renderer) bunları desteklemesi değişkendir ve [geçersiz kılma etiketlerini (override tags)]({{< relref "ASS_Tags" >}}) kullanmak hemen hemen her zaman daha iyi bir fikirdir. Bu alan genellikle otomasyon betikleri için bir meta veri alanı olarak kullanılır.
1. Bu altyazının en uzun satırındaki karakter sayısı.
1. Bu satırın katmanı. Bir [geçersiz kılma etiketi]({{< relref "ASS_Tags" >}}) ile konumlandırmayı değiştirip iki veya daha fazla satırın üst üste görüntülenmesini sağlarsanız, bu alan hangisinin nerede çizileceğini kontrol eder; yüksek katman numaraları daha düşük olanların üzerine çizilir.
1. Satırın başlangıç zamanı.
1. Satırın bitiş zamanı.
1. Satırın süresi. Bu alanı değiştirirseniz, bitiş zamanı buna bağlı olarak değişecektir.
1. Bu satır için sol kenar boşluğu. 0, stilde belirtilen kenar boşluğunun kullanılacağı anlamına gelir.
1. Bu satır için sağ kenar boşluğu. 0, stilde belirtilen kenar boşluğunun kullanılacağı anlamına gelir.
1. Bu satır için dikey kenar boşluğu. 0, stilde belirtilen kenar boşluğunun kullanılacağı anlamına gelir.
1. İmleç konumuna kalın yazı geçersiz kılma etiketi (`\b1`) ekler. Metin zaten kalınsa, karşılık gelen bir kapatma etiketi (`\b0`) ekler.
1. İmleç konumuna italik yazı geçersiz kılma etiketi (`\i1`) ekler. Metin zaten italikse, karşılık gelen bir kapatma etiketi (`\i0`) ekler.
1. İmleç konumuna altı çizili yazı geçersiz kılma etiketi (`\u1`) ekler. Metin zaten italikse, karşılık gelen bir kapatma etiketi (`\u0`) ekler.
1. İmleç konumuna üstü çizili yazı geçersiz kılma etiketi (`\s1`) ekler. Metin zaten italikse, karşılık gelen bir kapatma etiketi (`\s0`) ekler.
1. Bir yazı tipi seçim penceresi açar ve verilen yazı tipi adıyla bir yazı tipi yüzü etiketi (`\fnYazıTipiAdı`) ve seçilen efekt etiketlerini ekler.
1. [Renk seçiciyi]({{< relref "Colour_Picker" >}}) açar ve bir renk seçmenizi sağlar; ardından imleç konumuna seçilen renkle bir birincil renk geçersiz kılma etiketi (`\c`) ekler.
1. [Renk seçiciyi]({{< relref "Colour_Picker" >}}) açar ve bir renk seçmenizi sağlar; ardından imleç konumuna seçilen renkle bir ikincil renk geçersiz kılma etiketi (`\2c`) ekler.
1. [Renk seçiciyi]({{< relref "Colour_Picker" >}}) açar ve bir renk seçmenizi sağlar; ardından imleç konumuna seçilen renkle bir dış çizgi rengi geçersiz kılma etiketi (`\3c`) ekler.
1. [Renk seçiciyi]({{< relref "Colour_Picker" >}}) açar ve bir renk seçmenizi sağlar; ardından imleç konumuna seçilen renkle bir gölge rengi geçersiz kılma etiketi (`\4c`) ekler.
1. Bir sonraki satıra geçer, gerekirse dosyanın sonuna yeni bir satır oluşturur. Aegisub'ın önceki sürümlerinin aksine, değişikliklerin bu düğme kullanılarak işlenmesi (commit) gerekmediğine dikkat edin.
1. Görünümü zamanlar ve kareler arasında değiştirir. Bunun, zamanların betik içinde fiilen saklanma biçimini değiştirmediğine dikkat edin.

#### Orijinali Göster

"Orijinali Göster" kutusunu işaretlemek, düzenleme kutusunu şu moda geçirir:

![altyazı_düzenleme_kutusu_orijinal](/img/3.2/subs_edit_box_original.png)

Düzenleme kutusunun üst yarısı salt okunurdur ve şu anda seçili olan satırın ilk seçildiğindeki halini gösterir. Bu, altyazıları başka bir dile çevirmek veya sadece altyazıları düzenlemek için kullanışlı olabilir.

Geri Al
: Satırın metnini üst kutuda gösterilen metinle değiştirir. Fikrinizi değiştirirseniz satırda yaptığınız tüm değişiklikleri geri almanın basit bir yoludur.

Temizle
: Satırı temizler.

Metni Temizle
: Satırın metnini temizler ancak tüm geçersiz kılma etiketlerini yerinde bırakır. Çevrilmiş dizgileri başka bir dile çevirirken yardımcı olabilir.

Orijinali Ekle
: Satırın orijinal metnini imleç konumuna ekler.

#### Bağlam menüsü

Düzenleme kutusunda herhangi bir yere sağ tıklarsanız, şu menü görünür:

![altyazı_düzenleme_bağlam_menüsü](/img/3.2/Subs_Edit_Context.png)

Tümünü seç, kopyala, kes ve yapıştır beklediğiniz işlemleri yapar.

İmla denetimi
: Hatalı yazıldığı algılanan bir kelimeye sağ tıklarsanız, imla denetleyicisi bazı olası alternatifler önerir. Ayrıca bu menüden denetim için hangi dilin kullanılacağını ayarlayabilir veya tanınmayan ancak doğru yazıldığını bildiğiniz kelimeleri sözlüğe ekleyebilirsiniz. Aegisub'da imla denetimi hakkında daha fazla bilgi için [İmla Denetimi]({{< relref "Spell_Checker" >}}) sayfasına bakın.

Eş anlamlılar sözlüğü
: Vurgulanan kelimeye benzer alternatif kelimeler önerir.

Satırı böl
: Satırı, imleç konumunda iki yeni satıra böler. Zamanlamayı koru, her iki satır için de eski satırın zamanlamasını tutar. Zamanlamayı tahmin et, imlecin her iki tarafındaki metnin uzunluğuna dayanarak bölünmenin nerede olması gerektiğini tahmin etmeye çalışır. Video karesinde, satırın ilk yarısının önceki karede bitmesini, ikinci yarısının ise mevcut karede başlamasını sağlar.

### Altyazı ızgarası

![altyazı_ızgarası](/img/3.2/grid_context_menu.png)

Altyazı ızgarası, dosyadaki tüm satırları (yorumlar ve diğerleri) gösterir.

Bazı yaygın kontroller:

- Satırları ızgarada yukarı veya aşağı taşımak için onları seçin, Alt tuşunu basılı tutun ve yukarı veya aşağı ok tuşlarına basın.
- Birden fazla satır seçmek için Ctrl veya Shift tuşunu basılı tutarak tıklayın. Ctrl-tıklama, tıklama başına bir satır daha seçer; Shift-tıklama, ilk tıklanan ile son tıklanan arasındaki tüm satırları seçer.
- Seçimi değiştirmeden düzenleme kutusunda gösterilen aktif satırı değiştirmek için, Alt tuşunu basılı tutun ve yeni satıra tıklayın.
- Izgaradaki tüm satırları sıralamak için _Altyazı_ menüsünü açın ve _Satırları Sırala_ altında satırları sıralamak için kullanılacak alanı seçin.
- [Geçersiz kılma etiketlerinin]({{< relref "ASS_Tags" >}}) ızgarada görüntülenme biçimini değiştirmek için, araç çubuğundaki "etiket gizleme modları arasında geçiş yap" düğmesine tıklayın.

![altyazı_ızgarası_etiketleri](/img/3.2/subs_grid_tags.png)

Satırların, farklı şeyleri temsil eden (yapılandırılabilir) renkleri vardır; renklerin ne anlama geldiği hakkında ayrıntılar için [seçenekler sayfasının altyazı ızgarası bölümüne]({{< relref "Options#subtitle-grid" >}}) bakın.

Varsayılan olarak, şu sütunlar görünürdür:

**#**
: Satır numarası.

Başlangıç
: Satırın başlangıç zamanı.

Bitiş
: Satırın bitiş zamanı.

Stil
: Bu satır için kullanılan stil.

Metin
: Satırın metni (videoda görüntülenecek olan kısım).

Betiğin herhangi bir satırı kullanıyorsa, şu sütunlar da görüntülenir:

L
: Satırın katmanı (yukarıya bakın).

Oyuncu
: Satırı söyleyen oyuncu.

Efekt
: Bu satırın efekti.

Sol
: Sol kenar boşluğu.

Sağ
: Sağ kenar boşluğu.

Dikey
: Dikey kenar boşluğu.

Hangi sütunların görünür olacağını manuel olarak seçmek için ızgaranın en üst satırına (sütun adlarının olduğu satır) sağ tıklayabilirsiniz.

Izgaradaki herhangi bir satıra sağ tıkladığınızda şu menü açılır (seçeneklerin birçoğu diğer menülerde de mevcuttur):

![ızgara_bağlam_menüsü](/img/3.2/grid_context_menu.png)

Ekle (önce/sonra)
: Seçili satırdan önce veya sonra yeni bir boş satır ekler. Yeni satırın zamanlaması 0:00:00.00 ile 0:00:05.00 arasında ayarlanacaktır.

Video zamanında ekle (önce/sonra)
: Yukarıdakinin aynısıdır, ancak yeni satır mevcut video karesinde başlayacak şekilde zamanlanır. Video yüklü değilse etkin değildir.

Çoğalt
: Seçili satırı/satırları çoğaltır.

Mevcut kareden önce satırları böl
: Seçili satırı/satırları çoğaltır, orijinal satırın bitiş zamanını mevcut video karesinden bir önceki kareye ayarlar ve kopyanın başlangıç zamanını mevcut video karesine ayarlar. Kare kare dizgi yapmak ve bir satırı, artık görünmeyen bir satırla çakışıyorsa aşağı hareket etmesini sağlamak için sahne değişiminde bölmek için kullanışlıdır. Sadece video yüklü olduğunda etkinleşir.

Mevcut kareden sonra satırları böl
: Yukarıdaki gibidir, ancak mevcut kareden sonraki satır kısmını böler; satırın son karesinden ilk karesine doğru kare kare dizgi yaparken kullanılır.

Böl (karaoke ile)
: Satırı, karaoke geçersiz kılma etiketleri (`\k` ve türevleri) ile sınırlandırıldığı üzere hece başına bir yeni satıra böler. İlk satırın zamanlaması orijinal satırın başlangıç zamanında başlar ve o zamana ilk hecenin süresi eklenerek biter; takip eden satırlar, bir öncekinin bitişinde başlar ve hece süresi kadar devam eder.

Değiştir
: Seçili iki satırın (ızgaradaki) yerlerini değiştirir.

Birleştir (ilkini tut)
: İki veya daha fazla satırı birleştirir, ilk satır dışındaki tüm metinleri atar. Yeni satır, ilk satırın başlangıç zamanında başlayacak ve son satırın bitiş zamanında bitecek şekilde zamanlanır. Sadece birden fazla satır seçildiğinde etkinleşir.

Birleştir (art arda ekle)
: Yukarıdakiyle aynıdır ancak seçili tüm satırların metinlerini birleştirir. Her kaynak satırın metinleri arasına bir boşluk eklenir.

Birleştir (karaoke olarak)
: _Böl (karaoke ile)_ işleminin tersini yapar, yani _Birleştir (art arda ekle)_ ile aynıdır ancak birleştirilen satıra her kaynak satırın zamanlamasıyla `\k` etiketleri ekler.

Zamanlamaları sürekli yap (başlangıcı değiştir/bitişi değiştir)
: Seçili satırların zamanlamasını, her satırın bitiş zamanı bir sonrakinin başlangıç zamanı olacak şekilde değiştirir. Başlangıcı/bitişi değiştir, fonksiyonun her satırın bitiş zamanını mı yoksa başlangıç zamanını mı değiştireceğini belirler. Sadece birden fazla satır seçildiğinde etkinleşir.

Satırları yeniden birleştir
: Metnin bir kısmı iki veya daha fazla satırda kısmen mevcutsa, her metin parçası için bir satır oluşturur. Bu, genellikle şöyle görünen DVD'lerden kopyalanmış altyazıları düzeltmek için kullanışlıdır:

  ![Yeniden_Birleştir_01](/img/3.2/Recombine_01.png)

  Satırları yeniden birleştirdikten sonra sonuç şöyledir:

  ![Yeniden_Birleştir_02](/img/3.2/Recombine_02.png)

Ses klibi oluştur
: Yüklenen sesin, seçili satırların zamanlamasına karşılık gelen bir bölümünü (en erken başlangıç zamanından başlar ve en son bitiş zamanında biter) sıkıştırılmamış WAV dosyası olarak kaydeder. Sadece ses yüklü olduğunda etkinleşir.

Kes/Kopyala/Yapıştır
: Tüm satırları keser/kopyalar/yapıştırır. Satırların düz metin olarak kopyalandığını ve metin düzenleyiciler, sohbet programları, web tarayıcıları, diğer Aegisub örnekleri vb. arasında özgürce kopyalayıp yapıştırılabileceğini unutmayın.

Üzerine Yapıştır...
: [Üzerine Yapıştır]({{< relref "Paste_Over" >}}) diyaloğunu açar.

Sil
: Seçili satırları siler.