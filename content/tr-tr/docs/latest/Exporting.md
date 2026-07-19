---
title: Altyazıları Dışa Aktarma
menu:
  docs:
    parent: working-with-subtitles
weight: 3100
aliases:
  - /docs/latest/Exporting/
---

Normal "Kaydet" ve "Farklı Kaydet" işlevlerine ek olarak, Aegisub, tüm betiği çeşitli dışa aktarma filtreleri aracılığıyla dönüştürebilen bir "Dışa Aktar" özelliğine de sahiptir. Bu özellik, kare hızı dönüşümlerinden karaoke efektleri oluşturmaya, yalnızca başka biçimlere ve/veya karakter kümelerine kaydetmeye kadar bir dizi işlem için kullanılır.

## Dışa aktarma iletişim kutusu

![Dışa Aktar](/img/3.2/Export.png#center)

Pencerenin üst yarısı kullanılabilir filtreleri içerir. Bunlardan birini veya birkaçını işaretlemek, listelendikleri sırada uygulanmalarını sağlar; sırayı değiştirmek için yukarı/aşağı taşı düğmelerini kullanın. Alt yarı, seçilen filtrenin kısa bir açıklamasını içerir.

Bazı filtrelerin yapılandırma parametreleri vardır; bu parametrelere sahip olanlar pencereyi sağa doğru genişletir ve ilgili ayar kontrollerini buraya yerleştirir.

Alt kısımdaki açılır menü, dışa aktarılan dosya için hangi metin kodlamasının kullanılacağını kontrol eder. Unicode desteklemeyen eski programlara dışa aktarma yapmak için yararlı olabilir.

"Dışa Aktar" düğmesine tıkladığınızda, kaydetmek için ASS dışında başka biçimler de seçebileceğinizi unutmayın. Ayrıca bunun neredeyse her zaman birçok biçimlendirme etiketinin kaldırılacağı anlamına geldiğini de unutmayın.

## Filtreler

Varsayılan kurulumda aşağıdaki filtreler mevcuttur:

### Görünür satırlarla sınırla

Yalnızca aktif video karesinde o anda görünen satırları dışa aktarır. Video yüklü değilse hiçbir işlem yapmaz. Betik başlıkları ve stilleri vb. de dışa aktarılır.

### Karaoke şablonu

Karaoke efektleri oluşturmak için betiği "karaoke şabloncusu" otomasyon betiği aracılığıyla filtreler. Daha fazla ayrıntı için [karaoke şabloncusu]({{< relref "Automation/Karaoke_Templater" >}}) ve [otomasyona genel bakış]({{< relref "Automation" >}}) sayfalarına bakın.

### Kare hızını dönüştür

"Sabit" çıktı modunda, betikteki ( [geçersiz kılma etiketleri]({{< relref "ASS_Tags" >}}) içinde bulunanlar dahil) her bir zaman damgasını yeni bir kare hızıyla çalışacak şekilde yeniden hesaplar. Bunun, tüm betiğin "hızlandırılacağı" veya "yavaşlatılacağı" anlamına geldiğine dikkat edin. NTSC->PAL dönüşümleri veya tam tersi için kullanılabilir.

"Değişken" çıktı modunda, yüklü videonun (veya videodan farklıysa belirtilenin) kare hızını ve yüklü zaman kodlarını kullanarak betikteki her bir zaman damgasını yeniden hesaplar; böylece dışa aktarılan altyazılar yüklü video üzerine gömülebilir (hardsub) ve zaman kodları hesaba katıldıktan sonra yine de senkronize kalır. Zaman kodları yüklü değilse hiçbir işlem yapmaz. Daha fazla ayrıntı için [değişken kare hızlı video]({{< relref "Video#variable-framerate-video" >}}) sayfasına bakın.

### Etiketleri temizle

Betiği, geçersiz kılma etiketi bloklarını bitişik blokları birleştirerek ve gereksiz etiketleri (daha spesifik olarak, satır başına yalnızca bir kez belirtilebilen etiketlerin ikinci örneklerini) kaldırarak temizlemeye çalışan "etiketleri temizle" otomasyon betiği aracılığıyla filtreler.

### Betik bilgisini temizle

Betik başlıklarını, betiğin düzgün görüntülenmesi için kesinlikle gerekli olmayan tüm satırları kaldırarak temizler. Eğer bu konuda titizseniz, orijinal biçimde dağıtmayı planladığınız betikler için bunu kullanmayı düşünmelisiniz, çünkü Aegisub, son açılan video/ses dosyasına giden yol gibi şeyleri betik başlıklarında saklar.

### Stilleri düzelt

Betiğin tüm satırlarını gözden geçirir ve hangi stili kullandıklarını kontrol eder; mevcut betikte bulunmayan bir stili kullanan tüm satırlar "Default" (Varsayılan) stili ile değiştirilir.