---
title: Ses dosyasına göre zamanlama
menu:
  docs:
    parent: timing
weight: 5100
aliases:
  - /docs/latest/Timing/
---

## Ana ses ekranı

Ses dosyanız yüklendiğinde, Aegisub aşağıdaki ekran görüntüsüne benzer bir hale gelecektir:
![ses_görüntüsü](/img/3.2/audio_display.png)

Ses dalga formu/spektrum göstergesinin yüksekliğini değiştirmek için ses zaman çizelgesinin hemen altındaki alana tıklayıp sürükleyebilirsiniz.

Yeşil ve kırmızı düğmeler açma/kapama düğmeleridir. Yeşil arka plan seçeneğin açık olduğunu, kırmızı arka plan ise kapalı olduğunu gösterir. Düğmeler ve kontroller şöyledir (bunların çoğu varsayılan olarak [klavye kısayolları]({{< relref "Options#hotkeys" >}}) ile ilişkilendirilmiştir):

1. Kaydedilmemiş değişiklikleri atarak önceki satıra git ([karaoke modunda]({{< relref "Audio#karaokemode" >}}) önceki heceye git)
1. Kaydedilmemiş değişiklikleri atarak sonraki satıra git (karaoke modunda sonraki heceye git)
1. Ses dalga formunun seçili alanını çal
1. Mevcut seçili satırı çal
1. Oynatmayı duraklat
1. Seçim başlangıcından 500 ms önce çal
1. Seçim bitişinden 500 ms sonra çal
1. Seçimin ilk 500 ms'sini çal
1. Seçimin son 500 ms'sini çal
1. Seçim başlangıcından dosya sonuna kadar çal (veya duraklatılana kadar)
1. Giriş ekle (ne kadar olacağı [ses girişi ayarı]({{< relref "Options#audio" >}}) ile belirlenir)
1. Çıkış ekle (yukarıdakinin aynısıdır, ancak ayar mantıksal olarak [ses çıkışı]({{< relref "Options#audio" >}}) olarak adlandırılır)
1. Değişiklikleri onayla (kaydet)
1. Görünümü seçime kaydır/seçime git
1. Otomatik onayı aç/kapat (etkinleştirilirse, tüm zamanlama değişiklikleri kullanıcının onay düğmesine basmasını beklemeden anında kaydedilir)
1. Onaylandığında otomatik bir sonraki satıra geçmeyi aç/kapat (bu etkinleştirilirse, Aegisub geçerli satır kullanıcı tarafından onaylandığında otomatik olarak bir sonraki satırı seçer. Otomatik onaylar bariz nedenlerle bunu tetiklemez)
1. Otomatik kaydırmayı aç/kapat (etkinleştirildiğinde dalga formunu geçerli seçili satıra otomatik olarak ortalar)
1. Spektrum analizör modunu aç/kapat (aşağıya bakınız)
1. Medusa tarzı zamanlama kısayollarını aç/kapat
1. Karaoke modunu aç/kapat
1. Ses ekranı yakınlaştırma (yatay)
1. Ses ekranı yakınlaştırma (dikey)
1. Ses seviyesi
1. Dikey ses yakınlaştırma kaydırıcısının ses düzeyi kaydırıcısı ile bağlantısını aç/kapat

## Temel ses zamanlama

Altyazı ızgarasındaki bir satıra tıkladığınızda, Aegisub onu ses ekranında vurgulayacak ve otomatik kaydırma etkinse ses ekranını o satıra ortalayacak şekilde kaydıracaktır (normal zamanlama sırasında genellikle otomatik kaydırmayı devre dışı bırakmak iyi bir fikirdir). Ses ekranında çeşitli dikey çizgiler göreceksiniz; pembe olanlar, eğer yüklüyse videodaki anahtar kareleri (bkz. [Video ile çalışma]({{< relref "Video" >}}) bölümü), beyaz kesik çizgi mevcut görünür video karesini, kalın kırmızı ve turuncu çizgiler ise mevcut satırın (sırasıyla) başlangıç ve bitiş işaretçilerini gösterir. Satırın başlangıç ve bitiş zamanlarını (yeniden) tanımlamak için, başlangıç zamanını ayarlamak üzere sol tıklayıp bitiş zamanını ayarlamak üzere sağ tıklayabilir veya satır sınırlarını sürükleyip bırakabilirsiniz. Seçimi dinlemek için _çal_ düğmesine (varsayılan kısayol _s_), seçimin bölümlerini veya çevresindeki sesi dinlemek için diğer oynatma düğmelerine basın. Zamanlamadan memnun kaldığınızda, satırı kaydetmek ve bir sonrakine geçmek için onay düğmesine basın. Ardından her satır için bir kez tekrarlayın; bu kadar basit.

Shift tuşunu basılı tutmak, satır sınırlarının diğer satırlara ve anahtar karelere yapışmasını sağlar (veya varsayılan olarak yapışma ayarını yaptıysanız bunu devre dışı bırakır).
Ctrl tuşunu basılı tutmak, birden fazla çakışan sınırı aynı anda sürüklemenizi sağlar.
Örneğin, iki satır zaten birbirine hizalanmışsa ancak bunlar arasındaki geçişi biraz geriye kaydırmak istiyorsanız, ızgaradan her iki satırı da seçebilir, ardından ctrl tuşunu basılı tutup aralarındaki sınırı sürükleyerek hem ilk satırın bitiş zamanını hem de ikinci satırın başlangıç zamanını değiştirebilirsiniz.

Alt tuşunu basılı tutmak, tüm seçili satırları (hem başlangıç hem de bitiş zamanlarını) sürüklemenizi sağlar.

### Zamanlama ipuçları

Filminizi veya bölümünüzü makul bir süre içinde zamanlamayı bitirmek istiyorsanız dikkat etmeniz gereken bazı noktalar şunlardır:

- Klavye kısayollarını kullanın! Çalışmanızı birkaç kat hızlandırırlar.
- Zamanlama yaparken videonun görüntülenmesine gerek yoktur. Gerekli olduğunu düşünüyorsanız, muhtemelen yanlış bir şeyler yapıyorsunuz demektir. Sahne zamanlaması, yani satır başlangıç/bitişlerini sahne değişimlerine eşitleme, daha sonra yapılabilir. Ya manuel olarak ya da [zamanlama son işleyici]({{< relref "Timing_Post-Processor" >}}) ile.
- "Onaylandığında bir sonraki satıra geç" özelliğini kullanın.
- Yeni başladığınızda farklı zamanlama stilleriyle denemeler yapın ve size uyan birinde karar kılın. Sonra pratik yapın. Çokça.
- Aegisub büyük ölçüde "odak" kavramına dayanır ve video/ses/altyazı düzenleme kutusu arasında çok fazla geçiş yapmanızı gerektiren şekillerde çalışmak size çok zaman kaybettirir. Bunun yerine işlemi birkaç "geçişte" yapın.
- Spektrum analizör modu başta tuhaf görünür ancak özellikle arka plan gürültüsü olduğunda satırların (veya karaoke modunda kelimelerin) nerede başlayıp nerede bittiğini "görmeyi" genellikle çok daha kolaylaştırır.
- Pratikle, baştan sona zamanlama yapmak genellikle kötü zamanlamayı düzeltmekten daha hızlı ve kolaydır, çünkü kötü zamanlamayı düzeltmek her satır için düşünmek üzere az da olsa zaman harcamanızı gerektirir.
- Tüm zamanlama verilerini silip yeniden başlamak istiyorsanız, tüm satırları 9:59:59.99 geri kaydırmak için [zamanları kaydır iletişim kutusunu]({{< relref "Shift_Times" >}}) kullanmak basit bir yoldur.

Yaygın bir zamanlama stili (bu sayfanın yazarı tarafından tercih edilen) kabaca şöyledir: "Onaylandığında bir sonraki satıra geç" özelliğini açın ancak otomatik onayı, otomatik kaydırmayı ve Medusa zamanlama kısayollarını devre dışı bırakın. Sol elinizin dört ana parmağını s/d/f/g tuşlarında tutun. Baş parmağınızı kullanmayacaksınız, bu yüzden onunla ne isterseniz yapın. Sağ elinizi farede tutun. Şimdi dalga formunda (sol ve sağ tıklayarak) geçerli altyazı satırıyla eşleşen bir konuşma satırı içermesi muhtemel bir alan seçin ve dinlemek için _s_ tuşuna basın. Çalarken gerekirse başlangıç zamanını ayarlayın. Oynatma işaretçisi bitiş zamanı işaretini geçtiğinde, bitiş zamanını da ayarlayın. Daha fazla doğruluk gerekiyorsa, _d_ tuşuna basarak seçimin son 500 ms'sini, _q_ tuşuna basarak seçimin başlangıcından 500 ms öncesini, _w_ tuşuna basarak seçimin bitişinden 500 ms sonrasını veya _e_ tuşuna basarak seçimin ilk 500 ms'sini çalın. Deneyim kazandıkça, _d_ ve _q_ haricinde _s_ dışında pek bir şey kullanmayacaksınız. Zamanlamadan memnun kaldığınızda, değişiklikleri onaylamak ve bir sonraki satıra geçmek için _g_ tuşuna basın. _f_ tuşuna basarak ses ekranını ileri kaydırın. Geri kaydırmanız gerekirse _a_ tuşunu kullanın. Değişiklikleri onaylamadan bir sonraki veya önceki satıra gitmek için _z_ ve _x_ tuşlarını kullanın.

Bu stil, ellerinizi hiç hareket ettirmenize gerek kalmaması avantajına sahiptir. Biraz eğitimle çok hızlı olabilir; 25 dakikalık bir bölümün 350-400 satırlık diyalog ses zamanlaması 40 dakikadan kısa sürede kolayca yapılabilir ve daha az sözlü senaryolar bazen gerçek zamandan daha hızlı yapılabilir.

Elbette bu stil herkese rahat gelmeyebilir; hangisinin sizin için en iyisi olduğuna karar vermeden önce diğer zamanlama stillerini denemelisiniz.

### Spektrum analizör modu

![spektrum](/img/3.2/spectrum.png)

Spektrum analizör düğmesine bastığınızda, dalga formu dikey eksende artık genliği (sinyal gücünü) göstermez, bunun yerine frekansı gösterir. Yukarı çıkıldıkça frekans yükselir. Renkler ise genliği belirtir; siyah/koyu mavi sessizliği, beyaz ise en güçlü sesi temsil eder. Bu kafa karıştırıcı görünebilir ancak frekans penceresi insan seslerine oldukça uygun ayarlandığından, normal dalga formundan ayırt etmenin zor olduğu çok fazla arka plan gürültüsü (veya müzik) olduğunda bir satırın (veya karaoke modunda bir kelimenin) nerede başlayıp bittiğini anlamayı kolaylaştırabilir. Özellikle karaoke zamanlarken çok yararlı olabilir. Bir süre bununla oynarsanız nasıl çalıştığını anlayacaksınız.

Spektrum analizör modunda "dikey yakınlaştırma" kaydırıcısının, renkler sinyal gücünü belirttiği için renk yoğunluğunu kontrol edecek şekilde yeniden tanımlandığına dikkat edin.

Spektrum verilerini hesaplamak çok fazla CPU gerektirdiğinden, başlangıçta orta kalitede ayarlanmıştır. Spektrumun kalitesini [ses seçeneklerinden]({{< relref "Audio#options" >}}) artırabilirsiniz. Bu, çoğunlukla Aegisub'ı kendiniz derlediğinizde ve FFTW3 kullanmadığınızda önemlidir; FFTW3 o kadar hızlıdır ki varsayılan kalite biraz daha yüksektir.

## Karaoke zamanlama

[Karaoke zamanlama öğreticisi]({{< relref "Karaoke_Timing_Tutorial" >}})