---
title: Karaoke Zamanlama Eğitimi
menu:
  docs:
    parent: tutorials
weight: 2710
aliases:
  - /docs/latest/Karaoke_Timing_Tutorial/
---

Bu eğitim size Aegisub'a nasıl şarkı yükleneceğini, şarkı sözlerinin nasıl girileceğini ve sözleri şarkıyla senkronize etmek için nasıl zaman kodları ekleneceğini öğretecektir.

Bu eğitimi takip etmek için daha önce Aegisub kullanmış olmanıza gerek yoktur.

## Başlamadan önce

Başlamadan önce hazır bulundurmanız gereken birkaç şey var:

- Şarkının kendisi. Bu örneğin bir MP3 dosyası olarak veya bir videonun içinde olabilir. Aegisub sesleri video dosyalarından okuyabilir, şarkı bir videonun içindeyse ayrı bir ses dosyası oluşturmanıza gerek yoktur.

<div></div>

- Şarkının sözleri. Bunları zaten kıtalara ve mısralara ayrılmış düz bir metin dosyasında (.txt dosyası) bulundurmanız en kolayıdır.

<div></div>

Burada gösterim amacıyla İngilizce bir şarkı kullanıyorum ancak Aegisub'daki daha gelişmiş işlevlerin çoğu, genellikle transkripsiyon veya Latin alfabesine çeviri gerektiren Japonca ve diğer dillerdeki şarkılarla kullanılmak üzere tasarlanmıştır. Bunların nasıl kullanılacağını bir video eğitiminde göstereceğim.

## Şarkıyı yükleme

Yeni bir dosya oluşturarak başlayacağız. Aegisub'ı yeni başlattıysanız bu zaten elinizde mevcuttur.

![Karatiming-1](/img/3.2/Karatiming-1.png)

Şimdi şarkınızı açın. **Ses** menüsünden **Ses Aç** seçeneğini seçin...

![Karatiming-2](/img/3.2/Karatiming-2.png)

...ardından şarkı dosyanızı seçin.

![Karatiming-3](/img/3.2/Karatiming-3.png)

Aegisub şimdi ses dosyasını okumak için kısa bir süre harcayacaktır.

![Karatiming-4](/img/3.2/Karatiming-4.png)

İşlem bittiğinde, Aegisub penceresinin üst kısmında bir dalga biçimi görünümü (ses görünümü) olmalıdır. Daha önce Aegisub kullandıysanız işler biraz farklı görünebilir, ayarları bu resimdeki gibi yaparsanız eğitimin geri kalanını takip etmek daha kolay olabilir.

![Karatiming-5](/img/3.2/Karatiming-5.png)

Birazdan zamanlama için ses ekranının nasıl kullanılacağına bakacağız, ancak önce şarkı sözlerini yükleyelim.

### İpuçları

**Doğrudan video dosyalarından ses yükleme:** Ses Aç dosya seçicisinden video dosyalarını seçebilirsiniz. Bu aslında videonun kendisini açmaz, sadece video dosyasındaki sesi okur, tıpkı ayrı bir dosyadaki ses gibi.

**WAV dosyalarının anında yüklenmesi:** Sıkıştırılmamış bir PCM WAV dosyanız varsa, Aegisub bunu önce belleğe tamamen yüklemeden anında açabilir. Bu harika bir zaman kazandırıcı olabilir, ancak elbette biraz ekstra disk alanı ve muhtemelen WAV dosyasını oluşturmak için önceden biraz çalışma gerektirir. (Bunun yalnızca _sıkıştırılmamış PCM_ dosyalarıyla çalıştığını, WAV dosyalarındaki ADPCM veya MP3 gibi şeylerin çalışmayacağını ve yine de ön yüklemeyi tetikleyeceğini unutmayın.)

## Kelimeleri girme

Şimdi, metni içeri aktarmak için doğrudan yazmaya başlayabiliriz...

![Karatiming-6](/img/3.2/Karatiming-6.png)

**Ama bunu yapmayın!** Her şey bir metin dosyasında olursa, oradan kopyalayıp Aegisub'a yapıştırırsanız çok daha başarılı olursunuz. (Çoğu zaman doğrudan en sevdiğiniz şarkı sözü sitesinden de kopyalayıp yapıştırabilirsiniz.)

Şarkı sözlerim bir metin dosyasında var, bu yüzden onu açıyorum, metni seçiyorum ve panoya kopyalıyorum.

![Karatiming-7](/img/3.2/Karatiming-7.png)

Şimdi işler biraz karmaşıklaşıyor ama endişelenmeyin, gerçekten zor değil :-)

Aegisub'da yapıştırabileceğiniz iki farklı yer vardır: Altyazı tablosu ve altyazı düzenleme kutusu. Altyazı tablosuna yapıştırdığınızda altyazı dosyasında yeni satırlar oluşturursunuz. Altyazı düzenleme kutusuna yapıştırdığınızda ise o anda seçili olan altyazı satırını değiştirirsiniz.

Altyazı tablosuna yapıştırdığımızdan emin olmak istiyoruz, bu nedenle giriş odağını oraya ayarlamak için tablo alanının (pencerenin altındaki) içine bir kez tıklayın.

![Karatiming-8](/img/3.2/Karatiming-8.png)

Ve şimdi şarkı sözlerini yapıştırabiliriz.

![Karatiming-9](/img/3.2/Karatiming-9.png)

Tabloda hemen satırlar olarak görünmeleri gerekir. Hepsini başlangıç ve bitiş zamanlarının sıfıra ayarlandığına dikkat edin. Bu, şarkı sözlerinin her bir satırını şarkıyla zamanlayacağımız zaman işi kolaylaştırır.

![Karatiming-10](/img/3.2/Karatiming-10.png)

Dosyanızı şimdi kaydetmeniz iyi bir fikir olabilir, böylece daha sonra isim vermek zorunda kalmadan kolayca kaydedebilirsiniz.

Aegisub'ın henüz bir isim vermemiş olsanız bile dosyanızın bir kopyasını her dakika otomatik olarak kaydettiğini unutmayın, bu nedenle bir şeyler ters giderse nadiren çok fazla iş kaybedersiniz.

![Karatiming-11](/img/3.2/Karatiming-11.png)

Şimdi şarkı sözlerindeki her bir satırı zamanlamaya hazırız.

## Kaba zamanlama, önce satırlar

Zamanlamaya başlamadan önce, burada sunulan yöntemin birçok yöntemden yalnızca biri olduğunu bilmelisiniz. Aegisub'da sese göre zamanlama yapmanın birkaç yolu vardır ve bu sizin için en iyisi olmayabilir. Programı keşfetmeye çalışın ve kendi en iyi yolunuzu bulup bulamayacağınızı görün. Bu sadece benim (jfs) genellikle yaptığım yoldur.

Öncelikle ses ekranında nasıl gezineceğimize ve sesi nasıl oynatacağımıza bakalım. En az 6 farklı "Oynat" düğmesi olduğunu zaten fark etmiş olabilirsiniz. Ancak genellikle bunlardan yalnızca birini kullanırsınız: Çevresinde mavi dışa dönük parantezler olan. Bu "Seçimi Oynat"tır ve sesin o anda vurgulanmış olan kısmını oynatır.

![Karatiming-12](/img/3.2/Karatiming-12.png)

Seçimi Oynat düğmesine basmayı deneyin, şarkının ilk 5 saniyesinin çalındığını duymalısınız. (Aegisub varsayılan olarak ilk 5 saniyeyi seçer.)

Şimdi seçimi değiştirmeyi deneyin: Sürüklediğiniz bölümü seçmek için ses ekranında sol tıklayıp sürükleyebilirsiniz. Seçimin sol veya sağ kenarını tıklayıp sürüklerseniz yalnızca başlangıcı veya bitişi değiştirebilirsiniz. Son olarak, seçimin başlangıcını tam o noktaya ayarlamak için herhangi bir yere tek bir sol tıklama (sürüklemeden!) yapabilir ve seçimin bitişini ayarlamak için tek bir sağ tıklama yapabilirsiniz.

İlk satırı zamanlayalım. Üzerinde çalıştığınız şarkının ilk satırının başlangıcını ve bitişini bulun ve ses seçiminin bununla tam olarak eşleştiğinden emin olun. İlk başta seçimin gri olduğunu, ancak değiştirmeye başlar başlamaz kırmızıya döndüğünü ve "Modified" (Değiştirildi) kelimesinin göründüğünü fark edin. Bu, seçimi değiştirdiğiniz ancak yeni zamanlamayı kaydetmediğiniz (onaylamadığınız) anlamına gelir.

Zamanlamayı onaylamak ve altyazı satırına geri kaydetmek için yeşil onay işareti olan Onayla (Commit) düğmesine basmanız yeterlidir.

![Karatiming-13](/img/3.2/Karatiming-13.png)

Onayladığınızda otomatik olarak bir sonraki satıra da yönlendirilirsiniz, böylece hemen onu zamanlamaya devam edebilirsiniz.

Şarkının tüm satırlarını kapsayana kadar bu şekilde zamanlamaya devam edin: Satırın başlangıcını ve bitişini bulun, seçimi ayarlayın ve ardından onaylayın.

İşiniz bittiğinde dosyayı kaydedin.

### İpuçları

Sesten zamanlama yapmak hiç de zor değil, ancak bunu daha da kolay ve çok daha hızlı hale getirecek bazı ipuçları!

**Kısayol Tuşları:** Ses zamanlamasını çalışmayı çok daha hızlı hale getirebilecek bir dizi klavye kısayolu vardır.

![Karatiming-14](/img/3.2/Karatiming-14.png)

En önemlileri şunlardır:

- **S** - Seçimi Oynat: O anda seçili olan sesi oynatır.
- **A** ve **F** - Sola ve Sağa Kaydır: Sesin görünen kısmını değiştirir.
- **G** - Onayla (Commit): Mevcut ses seçiminin başlangıç ve bitiş zamanlarını altyazı tablosunda seçilen satıra kopyalar ve bir sonraki satıra geçer.

<div></div>

**Başlangıç/bitiş yakınını oynat:** Seçimin başlangıcından ve bitişinden hemen önce veya hemen sonra yarım saniye oynatan dört düğme (kısayol tuşları Q, W, E ve D) vardır. Başlangıç ve bitişi tam olarak şarkının başladığı/bittiği yere daha doğru bir şekilde ayarlamak için bunları kullanabilirsiniz.

**Oynatırken seçimi değiştirin:** Ses oynatılırken seçimi değiştirmeye devam edebilirsiniz. Seçim başlangıcını değiştirirseniz herhangi bir fark görmezsiniz, ancak seçim bitişini değiştirirseniz oynatma artık yeni seçim bitişine ulaştığında sona erecektir. Bu şekilde, bitişi oynatma imlecine (Aegisub oynatılırken hareket eden beyaz çizgi) yakın ayarlayarak oynatmayı hızlıca durdurabilir veya daha da ileri gitmesi için oynatmayı uzatabilirsiniz.

Örneğin, ilk satırın başlangıcını ararken, başlangıçtaki 5 saniyelik seçimle oynatmaya başlayabilir ve satırı bulana kadar uzatmaya devam edebilirsiniz. Ardından, hala oynatılırken doğru başlangıç zamanını ve ardından bitiş zamanını ayarlayabilirsiniz. Satırı yaklaşık olarak bu şekilde belirledikten sonra, seçimin tamamını tekrar oynatarak veya başlangıç ve bitiş zamanlarının hemen etrafındaki kısımları oynatmak için Q/W/E/D tuşlarını kullanarak ekstra bir kontrol yapabilirsiniz.

**Spektrum modu:** Genellikle ses ekranı dalga biçimi modundadır, şu ana kadar tüm ekran görüntülerinde gösterdiğim şey buydu. Ama aslında Aegisub'ın sesi göstermek için çok daha havalı bir yolu var: Spektrum modu.

![Karatiming-15](/img/3.2/Karatiming-15.png)

Spektrum modu, dalga biçimi modundan daha fazla CPU ve RAM tüketir, ancak sesin daha iyi bir resmini verir ve biraz pratikle şarkı söylemeyi müzikten ayırt etmeyi ve hatta farklı seslerin nasıl göründüğünü öğrenebilirsiniz. Örneğin, 'S' seslerini tanımak çok kolaydır.

**Yakınlaştırma ve ölçekleme:** Sesi yakınlaştırıp uzaklaştırmak ve ses seviyesini değiştirmek için ses ekranının en sağındaki kaydırıcı çubukları kullanabilirsiniz.

## Hassas zamanlama, önce kelimeler sonra heceler

{{<todo>}}
Karaoke düğmesine tıklayın.<br>
Kelimeleri zamanlayın.<br>
Böl (Split) düğmesine tıklayın. Bölme işaretlerini yerleştirin. Bölmeyi Kabul Et (Accept Split) düğmesine tıklayın.<br>
Heceleri zamanlayın.<br>
Onaylayın.<br>
Tekrarlayın.
{{</todo>}}

## Biçimlendirme

{{<todo>}}stiller, temel karaokenin nasıl göründüğü ve \kf ile \ko efektleri hakkında biraz bilgi {{</todo>}}

## Tamamlarken

{{<todo>}}video eğitiminden tekrar bahsedin ve diğer ilgili konulara işaret edin {{</todo>}}