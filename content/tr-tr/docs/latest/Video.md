---
title: Video ile Çalışmak
menu:
  docs:
    parent: typesetting
weight: 4100
aliases:
  - /docs/latest/Video/
---

Aegisub bir video (veya medya) oynatıcısı değildir, ancak yine de çeşitli yollarla video yüklemeyi ve video ile çalışmayı destekler. Bu sayfa, Aegisub'ın video yükleme ve işleme mekanizmasının bir referansıdır; sadece görüntülerin düzgün şekilde gösterilmesine dair daha basit bir giriş için [Görsel_Zamanlama]({{< relref "Visual_Typesetting" >}}) sayfalarını okumak isteyebilirsiniz.

## Video açma

Bir video dosyası yüklemek için _Video_ menüsüne gidin ve _Video dosyasını aç_ seçeneğine basın. Hangi video dosyalarını açabileceğiniz, [video sağlayıcınıza]({{< relref "Options#video" >}}) bağlıdır. Bir kukla (örnek, boş) video kullanmak için _Kukla video kullan_ seçeneğine basın.

### Desteklenen formatlar

Aegisub, normalde video açmak için neredeyse tüm yaygın A/V formatlarını ve pek çok nadir formatı destekleyen [FFMS2](https://github.com/FFMS/ffms2) kullanır. Desteklenen kodeklerin tam listesi için [FFmpeg](https://ffmpeg.org/) veya [Libav](https://libav.org/) belgelerine bakın. FFMS2'nin şu anda geçmeli (interlaced) H.264 ile ilgili sorunları olduğunu unutmayın.

Windows üzerinde, FFMS2 yerine [Avisynth](https://avisynth.org/mediawiki/Main_Page) kullanılabilir. _Avisynth_ aracılığıyla açarken, Aegisub en iyi seçeneği bulmak için birkaç kaynak işlevi deneyecektir:

Import()
: Avisynth yerleşik işlevi. Avisynth betiklerini yüklemek için kullanılır, başka hiçbir şey için kullanılmaz.

AviSource()
: Avisynth yerleşik işlevi. AviSource, videoyu açmak için sistemin Video for Windows (VfW) kod çözücüsünü kullanır; bu, bazı özel formatlar için dosyayı açmanın en iyi veya tek yolu olabilir. Bariz nedenlerden dolayı sadece .avi dosyalarını destekler. AviSource bir dosyayı açamazsa, sırasıyla DSS2 ve DirectShowSource denenir.

MPEG2Source()
: Sadece .d2v dosyalarını (DVD2AVI proje dosyaları; diğer adıyla DVD'lerden kopyalanmış indeksli .VOB'lar) yüklemek için kullanılır. Dosyayı açmak için neuron2'nin [DGDecode](https://neuron2.net/dgmpgdec/dgmpgdec.html) aracını kullanmaya çalışır; Aegisub bunu bulamaz veya yükleyemezse, bunun yerine eski mpeg2dec3.dll dosyasını dener; o da başarısız olursa bir hata döndürür. Bu, Aegisub'da DVD videosu açmanın en güvenilir yoludur.

DSS2()
: Haali'nin DirectShowSource2 eklentisini ([Haali Media Splitter](https://haali.cs.msu.ru/mkv/) paketi ve [CCCP](https://cccp-project.net) ile birlikte gelir; Avisynth eklentisi _avss.dll_ dosyasıdır, bunu Aegisub veya Avisynth'in bulabileceği bir yere manuel olarak yerleştirmeniz gerekir, aşağıya bakın) bulmaya, yüklemeye ve kullanmaya çalışır. Bu da, dosyayı açmak için bilgisayarınızın DirectShow ortamını kullanmaya çalışacaktır. Teorik olarak DirectShow tarafından işlenebilen her dosya desteklenmelidir, ancak üçüncü taraf ayırıcıların ve kod çözücülerin insafına kaldığınız için sonuçlar değişebilir. Genel bir kural olarak, Windows Media Player'da oynatılabiliyorsa, Aegisub onu açabilmelidir. DSS2'nin değişken kare hızı (VFR) dosyalarını sabit kare hızına (CFR) dönüştürdüğünü unutmayın. Genellikle istediğiniz ve beklediğiniz budur, ancak düzgün bir VFR altyazısı yapıyorsanız, bu durum uygun değildir.

DirectShowSource()
: Dosyayı yüklemek için (Avisynth ile gelen) DirectShowSource() işlevini kullanır. Temelde DSS2 ile aynıdır ancak çok daha az güvenilirdir ve VFR'yi CFR'ye dönüştürmez. Uyarı: DSS'nin kare bazında doğru arama (frame-accurate seeking) konusunda sorun yaşadığı bilinmektedir. Mümkünse kullanmayın.

[VFR]({{< relref "Video#variable-framerate-video" >}})'nin Avisynth sağlayıcısı tarafından desteklenmediğini unutmayın. Bazı durumlarda [harici zaman kodlarını]({{< relref "Video#timecodes" >}}) yüklemek işe yarayabilir, ancak pratikte bu genellikle bozuk bir sonuçla sonuçlanacaktır.

Aegisub, Avisynth eklentilerini kendi [?data]({{< relref "Aegisub_path_specifiers" >}}) dizininde (genellikle Windows'ta aegisub32.exe'nin bulunduğu klasör) arayacaktır. Ayrıca, otomatik olarak yüklenmelerini sağlamak için onları doğrudan Avisynth eklentileri klasörünüze de koyabilirsiniz.

### Kukla video

Aegisub, elinizde gerçek bir video dosyası olmasa bile altyazıları oluşturmanız (render) için sahte bir video yüzeyi sağlama özelliğini destekler. Kukla video iletişim kutusu şu şekilde görünür:

![Kukla video](/img/3.2/Dummy_video.png#center)

Çözünürlük (Resolution)
: Kukla videonun piksel cinsinden çözünürlüğü. Açılır menüde önceden tanımlanmış birkaç seçenek vardır; boyutu kendiniz de belirleyebilirsiniz. Kukla video RGB olduğu için tek sayılı genişlik/yüksekliklerle ilgili herhangi bir kısıtlama olmadığını unutmayın.

Renk (Colour)
: Video yüzeyinin rengi. Varsayılan olarak renk tek renktir; daha fazla çeşitlilik istiyorsanız "damalı desen" kutusunu işaretleyin.

Kare hızı (Frame rate)
: Saniye başına kare sayısı (fps) ayarlanarak her karenin ne kadar süre görüntüleneceğini belirler. Kukla video ile VFR zaman kodlarını yüklemenin aslında mümkün olduğunu unutmayın.

Süre (Duration)
: Videonun kare cinsinden süresi. Bu sayının altında, ortaya çıkan saat/dakika/saniye cinsinden toplam süre gösterilir.

## Video oynatma

Aegisub video oynatmayı destekler, ancak bunun bir özellik mi yoksa bir hata mı olduğu geniş çapta tartışılmıştır.

### "Oynat" düğmesine basmadan önce

İyice düşünün. Videoyu gerçekten oynatmak **istiyor musunuz?** (İpucu: Cevap "hayır", bunu yapmak istemezsiniz, en azından Aegisub içinde.) Eğer bir altyazının videodaki bir şeyle eşleşip eşleşmediğini kontrol etmeye çalışıyorsanız, yön tuşlarıyla videoda kare kare ilerlemek daha kolay olmaz mıydı? Eğer son okuma (proofreading) yapıyorsanız, bunu izleyicilerinizin gerçekte kullanabileceği bir oynatıcıda izlemek daha iyi bir fikir olurdu.

Sonuç olarak: gerçek dünya durumlarında, Aegisub içinden videoyu oynatmanıza asla gerek kalmayacaktır. Mantra şudur: Aegisub bir medya oynatıcısı değildir; eğer bir medya oynatıcısı istiyorsanız, bir medya oynatıcısı kullanın. Bununla birlikte, Aegisub güvenilir bir video oynatmayı desteklemek için makul bir çaba gösterir ve pratikte genellikle sorunsuz çalışır.

Video oynatılırken sesin duyulabilmesi için Aegisub'da sesin ayrıca yüklenmesi gerektiğini unutmayın. Bunu zahmetli buluyorsanız, bir video dosyası açıldığında sesin otomatik olarak açılmasını sağlayan bir seçenek mevcuttur.

## Ana kareler (Keyframes)

Video 101 dersini kaçıranlar için ana karenin ne olduğuna dair kısa, oldukça basitleştirilmiş bir açıklama:

Modern video kodekleri, mümkün olduğunca az bilgi depolayarak videoyu sıkıştırır. Tüm kareleri tam olarak saklamak yerine (çok miktarda JPG resmi gibi), ara sıra tamamen saklanan bir ana kare alırlar ve bir sonraki ana kareye kadar olan her kare için yalnızca son kareden bu yana neyin değiştiğini saklarlar. Bu nedenle, belirli bir kareye gitmek için kod çözücünün önceki ana kareyi bulması ve o kare ile hedef kare arasındaki tüm karelerin kodunu çözmesi gerekir; bu da ana karelere gitmenin diğer karelere gitmekten daha hızlı olduğu anlamına gelir. Ana kareler, genellikle sahne geçişlerinde göründükleri için çoğunlukla sahne zamanlaması nedeniyle önemlidir. Bir sahnedeki ilk kare neredeyse her zaman bir ana karedir, ancak dikkatli olun; her ana kare bir sahne geçişi değildir! Çoğu kodlayıcı, sahne geçişi olmasa bile en az 250-300 karede bir ana kare ekler.

Aegisub, ana kare verilerini programdaki çeşitli yerlerde kullanır. Bunlar video arama çubuğunda siyah çizgiler olarak çizilir ve (varsayılan olarak) ses dalga formu/spektrum analizöründe de görüntülenir.

### Ana kare verilerinin yüklenmesi ve kaydedilmesi

Videoyu FFMS2 aracılığıyla açarken, Aegisub çoğu dosya formatından ana kare verilerini okumayı desteklerken, Avisynth sağlayıcısı sadece AVI'den ana kare okumayı destekler. Ana karelerin okunamadığı bir video formatı kullanıyorsanız, ana kare verilerini yine de ayrı olarak yükleyebilirsiniz. Aegisub şu anda birkaç formattan okumayı desteklemektedir: kendi ana kare dosya formatı (aşağıdaki teknik özelliklere bakın), XviD ilk geçiş (first-pass) dosyaları, DivX ilk geçiş dosyaları ve x264 ilk geçiş dosyaları.

Dosyadan ana kareler okunabilse bile, bazen bunları harici ana karelerle geçersiz kılmak yararlıdır. XviD'in ana kare seçimleri sahne değişiklikleriyle alışılmadık derecede iyi bir korelasyon gösterdiğinden, ses zamanlaması için XviD ilk geçiş .stat dosyalarını kullanmak oldukça popülerdir.

Aegisub ayrıca şu anda yüklü olan ana kare verilerini bir ana kare dosyasına yazabilir; bu, belirli durumlarda (örneğin ses zamanlaması) video dosyalarını taşımaktan kaçınmak için yararlı olabilir.

### Ana kare dosya teknik özellikleri

Bir ana kare dosyası, düz ASCII kodlu bir metin dosyasıdır; hem \n hem de \r\n satır sonu olarak anlaşılır. Sözdizimi örneği:

```plaintext
# keyframe format v1
fps 0
0
30
70
82
130
131
```

İlk satır biçim belirtimidir: `# keyframe format v1` dizisi. İkinci satır, ana kare verilerini oluşturmak için kullanılan videonun FPS değerini içerir; ancak hiçbir program (Aegisub dahil) bunu gerçekten desteklemez ve bu nedenle genellikle sadece `0` değerindedir. Son olarak, fps satırından sonra isteğe bağlı sayıda uzun tamsayı (satır başına bir tane) gelir ve her biri bir ana karenin kare numarasını temsil eder. Kare numaraları sıfır tabanlıdır; yani videonun ilk karesi 0 numaralı karedir.

## Değişken kare hızlı (VFR) video

Aegisub, değişken kare hızlı video yüklemeyi ve bunlarla çalışmayı destekler. VFR'nin nasıl ve nedenleri bu kılavuzun kapsamının çok dışındadır (daha fazla bilgi için örneğin [AnimeSuki'deki VFR başlığına](https://forums.animesuki.com/showthread.php?t=34738) veya [Avisynth kılavuz sayfasına](https://avisynth.org/mediawiki/VFR) bakın), ancak Aegisub'ın bunu nasıl ele aldığı hakkında bilmeniz gerekenleri burada ele alacağız.

### Zaman kodları

Matroska zaman kodu dosyalarının (v1 ve v2) yüklenmesi desteklenir ve eğer VFRaC (Sabit kabul edilen Değişken Kare Hızı; örneğin sabit bir FPS'deki AVI içinde saklanan VFR MKV'nin kareleri, ayrıntılar için yukarıda bağlantısı verilen VFR başlığına bakın) bir video dosyanız varsa ancak altyazıların buna senkronize olmasını istiyorsanız yararlıdır. Bir VFR dosyası yüklerseniz, Aegisub zaman kodlarını doğrudan dosyadan otomatik olarak okuyacaktır.

### VFR ve kalıcı altyazı (Hardsubbing)

GDSMux ile kodlama yapmadığınız sürece, altyazı filtrenizin çalıştığı kodlama ortamı (yani Avisynth, VirtualDub veya mencoder) dünyanın CFR olduğunu ve dolayısıyla giriş dosyasının VFRaC olduğunu varsayacaktır. Altyazı senkronizasyonunu bozduğu için bu açıkça bir sorundur. Aegisub, VFRaC giriş dosyasının kare hızını ve zaman kodlarını alan ve ardından altyazıların VFRaC videosuna kalıcı olarak gömülebilmesi (hardsub) ve zaman kodları uygulandıktan sonra bile mükemmel şekilde senkronize kalabilmesi için betikteki her zaman kodunu ve geçersiz kılma etiketini (override tag) değiştiren "Kare Hızı Dönüştürme" (Framerate Transformation) dışa aktarma filtresi aracılığıyla bunu aşmanın bir yolunu sunar. Bir betiği kalıcı altyazı için hazırlamak için zaman kodlarının yüklü olduğundan emin olun, ardından _Dosya_ menüsüne gidin ve _Dışa Aktar_ seçeneğine basın. _Kare Hızını Dönüştür_ filtresi dışındaki her şeyin işaretini kaldırın. _Değişken_ çıktı modunu seçin. Altyazıları kalıcı olarak gömeceğiniz videonun FPS'sini bilmesi gerekir; eğer videonuz yüklüyse Aegisub bunun o olduğunu varsayacak ve sizin için kutuya yerleştirecektir.

**Not:** Matroska veya başka bir VFR dosyanız yüklüyse, Aegisub'ın bildirdiği FPS değerinin altyazıları kalıcı olarak gömeceğiniz videonunkinden farklı olabileceğini unutmayın.

## Anamorfik video

**VEYA: Altyazılarınızın gerilmiş görünmemesini nasıl sağlarsınız?**

Aşağıdaki paragraflar, anamorfik videonun ne olduğu ve en boy oranlarının nasıl çalıştığına dair temel bir bilgiye sahip olduğunuzu varsayar. Emin değilseniz, [nazik ama oldukça eksiksiz bir giriş](https://www.hometheaterhifi.com/volume_6_4/feature-article-enhanced-widescreen-november-99.html) bölümüne göz atmak isteyebilirsiniz.

### Görüntü gerilmesi ve altyazı oluşturma

Anamorfik bir görüntünün izleyiciye sunulmadan önce uygun en boy oranına gerilmesi gerekir. Bir bilgisayarda bu genellikle video oluşturucu (video renderer) tarafından yapılır ve sorun burada yatar. Çoğu altyazı oluşturucu (mevcut "standart" oluşturucu olan VSFilter dahil), altyazı çizimini görüntü gerilmeden önce yapar ve oluşturucu herhangi bir en boy oranı sorununun farkında olmadığı için, video izleyiciye görüntülendiğinde altyazılar görüntüyle birlikte gerilir ve bu nedenle gerilmiş görünürler. Aegisub da altyazı oluşturma işlemini bu şekilde yapar (çünkü bu şekilde çoğu oynatıcıyla WYSIWYG olacaktır); nasıl göründüğünü video menüsündeki "En boy oranını geçersiz kıl" seçeneğini kullanarak test edebilirsiniz.

### Gerilmeye karşı telafi etme

Neyse ki, görüntünün ne kadar gerileceğini bildiğiniz için (orijinal boyutlarını ve görüntü en boy oranını bildiğinizden) gerilmeyi telafi etmek kolaydır. Görüntünün X veya Y yönünde yüzde kaç gerileceğini hesaplarsınız ve ardından [stildeki]({{< relref "Styles" >}}) ScaleX veya ScaleY parametresini (veya `\fscx` veya `\fscy` [geçersiz kılmalarını]({{< relref "ASS_Tags" >}}) kullanın) aynı miktarda ancak diğer yönde olacak şekilde ayarlarsınız.

Örnek: 16:9 (veya 1.7777...:1) olarak görüntüleneceğini bildiğimiz 704x480'lik bir görüntümüz var. Oynatıcının genişliği gereceğini ancak yüksekliği değiştirmeden bırakacağını varsayarsak, yeni genişlik şu olacaktır:

```plaintext
(16 / 9) * 480 = 853.333...
```

bu da yüzde olarak şöyledir:

```plaintext
853.333... / 704 = 1.212121...
```

yani %121. Bu nedenle, bu yatay (X yönü) gerilmeyi telafi etmek için, altyazıları aynı miktarda germek üzere tüm stillerimizdeki ScaleY değerini %121 olarak ayarlarız ve oluşturma işleminden sonra artık gerilmiş görünmezler.

**VEYA** oynatıcının görüntünün yüksekliğini değiştirdiğini varsayarak gerilmeyi diğer yönde yapabiliriz. Aynı görüntü varsayıldığında:
704 / (16 / 9) = 396
bu şuna karşılık gelir:
396 / 480 = 0.825
veya %82.5, yani ScaleX'i %82.5 olarak ayarlayarak dikey (Y) sıkıştırmayı telafi edebiliriz.

### Uyarılar

Yukarıdaki yöntemlerin her ikisi de altyazılara uygun en boy oranını verir, ancak oynatıcının gerilmeyi nasıl yaptığına bağlı olarak altyazı boyutunda küçük farklılıklar olabilir. Aegisub (ve aslında çoğu video oynatıcı ve oluşturucu), "özel" en boy oranını seçip bir çözünürlük belirtmediğiniz sürece her zaman görüntü genişliğini değiştirir, yüksekliğini asla değiştirmez. Matroska kabını kullanırsanız, görüntü çözünürlüğünü doğrudan belirtebileceğinizi unutmayın, ancak oynatıcı desteği buna göre değişir.

Bazı garip altyazı oluşturucuların (özellikle Media Player Classic'in yerleşik oluşturucusu) aslında video oluşturucunun bir parçası olduğunu ve altyazı oluşturma işlemini anamorfik gerilmeden _sonra_ yapacağını, bunun da gerilmiş altyazılara ve çok fazla rahatsızlığa neden olacağını unutmayın. MPlayer'ın libass oluşturucusu ile, altyazı oluşturucuyu filtre zincirinde hareket ettirmek için -vf parametresini kullanarak altyazıların gerilmeden önce mi yoksa sonra mı çizilmesi gerektiğini belirleyebilirsiniz.

### Daha fazla okuma

Anamorfik video ve genel olarak en boy oranları (bir bakışta basit görünen ancak derinlemesine gizlenmiş bir konu) hakkında daha fazla bilgi için aşağıdaki bağlantılar ilginizi çekebilir:

- [Dijital Video Çözünürlüğü ve En Boy Oranı Dönüşümlerine Kısa Bir Kılavuz](https://lipas.uwasa.fi/~f76998/video/conversion/) - Konuyu gerçekten anlamak isteyen herkes için kesinlikle temel bir okuma, ancak ne yazık ki çoğu insanın bu konuda bilmek isteyeceğinden çok daha fazlasını içeriyor.
- [Widescreen.org: En Boy Oranları](https://www.widescreen.org/aspect_ratios.shtml) - bazı yaygın en boy oranlarının geçmişi ve nedenleri
- [Wikipedia: En Boy Oranı (görüntü)](<https://en.wikipedia.org/wiki/Aspect_ratio_(image)>)
- [Wikipedia: Anamorfik Geniş Ekran](https://en.wikipedia.org/wiki/Anamorphic_widescreen)

## Video menüsü

Video menüsünden aşağıdaki seçenekler mevcuttur:

### Kaynak dosyası ile ilgili

Video aç
: Videoyu açar. Zaten yüklü bir video varken başka bir video açmaya çalışırsanız, orijinal videonun önce kapatılacağını unutmayın.

Videoyu kapat
: Şu anda açık olan videoyu kaldırır.

Son kullanılanlar
: Son açılan videoların listesini gösterir.

Kukla video kullan
: Bir kukla video açar (yukarıya bakın).

Video ayrıntılarını göster
: Şu anda açık olan video hakkında bazı bilgiler gösterir. Gösterilen ayrıntılar dosya adı, saniye başına kare sayısı (VFR dosyaları için ortalama FPS görüntülenir), çözünürlük ve en boy oranı, uzunluk ve kod çözücüdür. Kod çözücü, Aegisub'ın dosyayı açmak için kullandığı filtre/yöntemdir.

### Zaman kodları ile ilgili

Zaman kodu dosyası aç
: Bir zaman kodu dosyası yükler ve bunu videoya uygular, video/altyazı senkronizasyonunu değiştirir.

Zaman kodu dosyası kaydet
: Şu anda yüklü olan zaman kodlarını yeni bir v2 zaman kodu dosyası olarak kaydeder.

Zaman kodu dosyasını kapat
: Şu anda yüklü olan zaman kodlarını kaldırır.

Son kullanılanlar
: Son açılan zaman kodu dosyalarının listesini gösterir.

### Ana kareler ile ilgili

Ana kareleri aç
: Verilen dosyadan ana kare verilerini yükler. Zaten yüklü ana kare verileriniz varsa, dosyadakilerle değiştirilecektir.

Ana kareleri kaydet
: Şu anda yüklü olan ana kare verilerini bir ana kare dosyasına kaydeder.

Ana kareleri kapat
: Varsa, şu anda yüklü olan ana kare verilerini kaldırır. Doğrudan video dosyasından yüklenen ana kare verilerini kaldırmanın mümkün olmadığını unutmayın; herhangi bir nedenle bundan kurtulmak istiyorsanız, sadece 0. karesi ana kare olarak işaretlenmiş bir ana kare dosyası yükleyin.

Son kullanılanlar
: Son yüklenen ana kare dosyalarının listesini gösterir.

### Görüntüleme ile ilgili

Videoyu ayır
: Video ekranını ve ilgili kontrolleri Aegisub ana penceresinden ayırır ve kendi penceresine taşır. Videoyu tekrar ana pencereye eklemek için ayrılan pencereyi kapatın. Bu özellik özellikle çoklu monitör kurulumlarında yararlı olabilir.

Yakınlaştırmayı ayarla
: Video yakınlaştırma düzeyini ayarlar.

En boy oranını geçersiz kıl
: Video genişliğini değiştirerek videoyu belirtilen en boy oranına gerer. Anamorfik video için yararlıdır (yukarıya bakın).

Overscan maskesini göster
: Görüntü üzerine, aksiyon güvenli (koyu mavi) ve başlık güvenli (açık mavi) alanların kenarlarını gösteren mavi bir "maske" çizer. Altyazılarınızı ayarlanabilir bir overscan düzeltmesi olmayan bir TV'de göstermeyi planlıyorsanız yararlıdır. Daha fazla bilgi için [overscan](https://en.wikipedia.org/wiki/Overscan), [güvenli alanlar](https://en.wikipedia.org/wiki/Safe_area) ve [overscan miktarları](https://en.wikipedia.org/wiki/Overscan_amounts) ile ilgili Wikipedia sayfalarına bakın. Aegisub, güvenli alanların ne kadar büyük olması gerektiği konusunda [BBC yönergelerini](https://www.bbc.co.uk/guidelines/dq/pdf/tv/tv_standards_london.pdf) izler.

### Arama ile ilgili

Git
: Videoyu belirtilen zamana veya kareye götürür.

Videoyu başlangıca götür
: Videoyu o anda aktif olan satırın başlangıç zamanına götürür.

Videoyu sona götür
: Videoyu o anda aktif olan satırın bitiş zamanına götürür.