---
title: Altyazılar nesnesi
menu:
  docs:
    parent: lua-reference
weight: 6220
aliases:
  - /docs/latest/Automation/Lua/Subtitle_file_interface/
---

Bu sayfa, Automation 4 Lua betiklerinde altyazı dosyalarını işlemek için kullanılan **altyazı dosyası arayüzünü** açıklamaktadır.

Bir dizi işleve ve tanımlanmış tablo biçimine sahip özel bir nesne (**altyazılar** kullanıcı verisi nesnesi) mevcuttur.

## Altyazılar nesnesi

Çoğu Automation 4 Lua özellik işlevi, çağrıldığında bir **altyazı nesnesi** alır. Bu nesne, özelliğin uygulandığı altyazılardan veri almak ve bunları işlemek için kullanılır.

Bir altyazı nesnesi, oluşturulduğu bağlama bağlı olarak iki özel özelliğe sahip olabilir:

Salt okunur
: Bazı özellik işlevlerinin altyazı dosyasını hiçbir şekilde değiştirmesine izin verilmemelidir. Buna örnek olarak [makro doğrulama işlevleri]({{< relref "Registration#macro-validation-function" >}}) ve [dışa aktarma filtresi yapılandırma paneli sağlayıcıları]({{< relref "Registration#export-filter-configuration-panel-provider" >}}) dahildir, çünkü bu durum kullanıcı beklentilerinin dışındadır.

Geri alma noktalarına izin ver
: Sadece [makro işleme işlevleri]({{< relref "Registration#macro-processing-function" >}}) geri alma noktaları belirleyebilir, çünkü başka bir zamanda bunu yapmanın bir anlamı yoktur.

Maksimum esnekliği sağlamak için, altyazı nesnesi tüm meta satırları (bölüm başlıkları gibi) dahil olmak üzere satır satır eksiksiz bir ASS biçimli dosyayı temsil eder.

Altyazı nesnesi aşağıdaki işlemleri destekler:

- Satır sayısını alma
- Satır okuma
- Satır ekleme (dosyanın sonuna)
- Satır ekleme (dosyada herhangi bir konuma)
- Satır değiştirme
- Satır silme
- Geri alma noktası oluşturma

Bu işlemler aşağıda ayrıntılı olarak açıklanmıştır. Tüm işlem özetlerinde ve örneklerinde, üzerinde çalışılan altyazı nesnesinin adı olarak `subtitles` kullanılmıştır.

### Satır sayısını alma

Özet:

- `num_lines = #subtitles`
- `num_lines = subtitles.n`

Bu işlem, altyazı dosyasındaki mevcut toplam satır sayısını alır. Bu sayı sadece altyazı nesnesi üzerindeki diğer işlemler kullanılarak değişir. Bir betiğin yürütülmesi sırasında kendiliğinden değişemez.

Bunun sabit zamanlı bir arama olmadığını, ancak `for i = 1, #subs` şeklinde kullanıldığında Lua'nın değeri önbelleğe aldığını unutmayın.

`num_lines` (`number`)
: Altyazı dosyasındaki satır sayısı.

İlk sözdizimi, normal Lua 5.1 kodlama tarzına göre tercih edilen yöntemdir.

### Satır okuma

Özet: `line = subtitles[i]`

Bu, indekslenmiş satırı alır ve onun hakkında veriler içeren yeni bir tablo nesnesi oluşturur.

`line` (`table`)
: Alınan satır hakkındaki verileri içeren tablo.

`i` (`number`)
: Alınacak satır numarasının altyazı dosyasındaki indeksi. Bu indeks bire-dayalıdır, yani dosyadaki ilk satırın indeksi 1'dir.

Aegisub, altyazı dosyasını dahili olarak bir bağlı liste olarak saklar, bu da rastgele erişimin yavaş, ancak ardışık erişimin hızlı olduğu anlamına gelir. Automation 4 Lua, altyazıları bir diziymiş gibi sunsa da, ardışık erişimi optimize etmek için dahili olarak bir imleç tutar. Son eriştiğiniz satıra yakın bir indekse sahip bir satıra erişmek, daha uzaktaki bir satıra erişmekten daha hızlıdır. Dosyanın başına veya sonuna yakın satırlara erişmek her zaman hızlıdır.

### Satır ekleme (Sona)

Özet:

- `subtitles[0] = line`
- `subtitles.append(line)`
- `subtitles.append(line1, line2, ...)`

Altyazı dosyasının ilgili bölümünün sonuna bir veya daha fazla satır ekleyin. Bölüm mevcut değilse oluşturulacaktır. İlk sözdiziminde, indeks için 0 (sıfır) sayısı kullanılır. (0 indeksini ayarlamak bir ekleme işlemini tetikler.)

Üçüncü sözdizimi, tek bir işlemle birden fazla satır eklemeyi destekler.

`line` (`table`)
: Altyazı dosyasına eklenecek satır nesnesi tablosu.

Okunabilirlik açısından ikinci işlev çağrısı sözdizimi tercih edilir. Tablo indeksi ayarlama sözdizimi biraz daha hızlıdır.

Bir satır eklemek, ardışık erişimi optimize etmek için kullanılan imleci hareket ettirmez.

### Satır ekleme (Araya)

Özet:

- `subtitles[-i] = line`
- `subtitles.insert(i, line)`
- `subtitles.insert(i, line1, line2, ...)`

Altyazı dosyasına numaralandırılmış satırdan önce bir veya daha fazla satır ekler. İlk sözdiziminde negatif bir indeks sağlarsınız. Örneğin, 5. satırdan önce bir satır eklemek için -5 indeksini sağlarsınız.

Satır eklemek, eklenen satırlardan sonraki satırların indekslerinin aşağı kaymasına neden olur, bu nedenle eski indeksler artık geçerli olmayacaktır.

Altyazı dosyasının yanlış bölümüne satır eklemenin sonuçları tanımsızdır ve garip şekillerde bozulmalara yol açabilir.

`i` (`number`)
: Önüne ekleme yapılacak indeks.

`line` (`table`)
: Altyazı dosyasına eklenecek satır nesnesi tablosu.

Okunabilirlik açısından ikinci işlev çağrısı sözdizimi tercih edilir. Tablo indeksi ayarlama sözdizimi biraz daha hızlıdır.

Satır ekleme işlemi liste imlecini kullanır ve onu hareket ettirir.

### Satır değiştirme

Özet: `subtitles[i] = line`

İndekslenen satırı siler ve yerine verilen satırı ekler.

`i` (`number`)
: Değiştirilecek satır indeksi.

`line` (`table`)
: Yerine koyulacak satır nesnesi tablosu.

Satır değiştirme işlemi liste imlecini kullanır ve onu hareket ettirir.

Satırları farklı türdeki satırlarla değiştirmek tanımsız sonuçlar doğurur ve garip şekillerde bozulmalara neden olabilir.

### Satır silme

Özet:

- `subtitles[i] = nil`
- `subtitles.delete(i)`
- `subtitles.delete(i1, i2, ...)`
- `subtitles.delete({i1, i2, ...})`
- `subtitles.deleterange(first, last)`

Altyazı dosyasından bir veya daha fazla satırı kaldırın. Silinen satırdan/satırlardan sonraki tüm satırlar, silinen indeksleri doldurmak için yukarı kayacaktır, bu nedenle eski indeksler artık geçerli olmayacaktır.

Üçüncü sözdizimi, tek bir çağrıda birden fazla indekslenmiş satırı silmeyi destekler. Verilen indekslerin tümü, herhangi bir satır silinmeden önce altyazı dosyasının durumu için doğru olmalıdır.

Dördüncü sözdizimi `subtitles.delete(unpack(tbl))` ile aynıdır, ancak paketini açamayacak kadar büyük tabloları destekler ve satırlar zaten bir tabloda mevcutsa biraz daha hızlı çalışır.

Var olmayan bir satırı silmeye çalışmak, deleterange haricinde bir hatadır.

Beşinci sözdizimi, her iki indeksli satır dahil olmak üzere bir satır aralığını siler.

`i` (`number`)
: Silinecek satırın indeksi.

`first` (`number`)
: Silinecek aralığın ilk satırının indeksi.

`last` (`number`)
: Silinecek aralığın son satırının indeksi.

Satır silme işlemi liste imlecini kullanır ve onu hareket ettirir.

### Geri alma noktası oluşturma

Özet: `aegisub.set_undo_point(description)`

Altyazı nesnesinde değişiklik yapan herhangi bir makronun sonunda her zaman bir geri alma noktası oluşturmalısınız. Oluşturmazsanız, sizin için otomatik olarak bir tane ayarlanacaktır, ancak Aegisub'ın gelecekteki sürümlerinde bu durum, yapılan tüm değişiklikleri geri alma şeklinde değişebilir.

Tek bir makroda birden fazla geri alma noktası ayarlayabilirsiniz, ancak bunu yapmak nadiren iyi bir fikirdir.

Sadece makro işleme işlevlerinde kullanılabilir, çünkü başka hiçbir yerde bir anlamı yoktur.

`description` (`string`)
: Düzen menüsünde Geri Al ve Yinele öğelerinde, geri alınabilecek eylemi tanımlamak için görünecek metin.

Bu aslında altyazılar nesnesindeki bir işlev değildir, ancak yine de ona sıkı sıkıya bağlıdır.

## Satır veri tabloları

Altyazı dosyası nesnesinden satırları okuduğunuzda bunlar her zaman belirli sınıflardan biri olacaktır ve satırları altyazı dosyasına geri yazdığınızda, bu sınıflardan birinin biçimini takip etmeleri gerekir.

Satır veri nesneleri, tanımlanmış bazı belirli alanlara sahip normal Lua tablolarıdır.

İşte farklı satır sınıflarının listesi:

`info`
: Dosyanın Script Info bölümündeki bir anahtar/değer çifti

`style`
: Normal bir stil tanımı satırı

`dialogue`
: Yorum olabilir veya olmayabilir bir diyalog satırı. Bunlar Aegisub'daki kılavuzda gördüğünüz satırlardır.

`unknown`
: Bilinmeyen türde bir satır.

Tüm satır veri tablolarında her zaman var olan üç alan vardır:

`class` (`string`)
: Bu satırın ait olduğu sınıfın adı, yukarıdaki listeye bakın.

`raw` (`string`)
: Fiziksel satırdaki ilk karakterden son karaktere kadar olan ham metin.

`section` (`string`)
: Satırın dosyanın hangi bölümüne ait olduğu. Satır, ilk bölüm başlığından önce yerleştirilmişse, bu alan `nil` olur.

### `info` sınıfı

Bu sınıf iki ek alan tanımlar:

`key` (`string`)
: Satırın ilk iki noktadan önceki kısmı, baştaki ve sondaki boşluklar kaldırılmış haldedir.

`value` (`string`)
: Satırdaki ilk iki noktadan sonraki her şey, yine baştaki ve sondaki boşluklar kaldırılmış haldedir.

### `style` sınıfı

Bu sınıf çok sayıda ek alan tanımlar. Genellikle _karaskel_ tarafından işlenir ve bu süreçte biraz değiştirilir. Bu sınıf hakkında daha fazla bilgi için _karaskel.lua_ bölümündeki [stil tablolarına]({{< relref "Modules/karaskel.lua.md#style-table" >}}) bakın.

### `dialogue` sınıfı

Bu sınıf çok sayıda ek alan tanımlar. Genellikle _karaskel_ tarafından işlenir ve bu süreçte birçok hesaplanmış alan eklenir. Bu sınıf hakkında daha fazla bilgi için _karaskel.lua_ bölümündeki [diyalog satırı tablolarına]({{< relref "Modules/karaskel.lua.md#dialogue-line-table" >}}) bakın.

### `unknown` sınıfı

Doğası gereği bu sınıf tarafından tanımlanan hiçbir ek alan yoktur. Bunlar, altyazılara gömülmüş dosyalar gibi şeyler olabilir. Ne yaptığınızı gerçekten bilmiyorsanız bu satırlarla çalışmaya çalışmamalısınız. `unknown` satırlarını silmenin, değiştirmenin ve eklemenin tanımsız sonuçları vardır. (Yani, bugün çalışsa bile yarın veya Aegisub'ın bir sonraki sürümünde çalışmayabilir.)