---
title: Betik Çözünürlüğü
menu:
  docs:
    parent: miscellaneous
weight: 7400
aliases:
  - /docs/latest/Script_Resolution/
---

ASS altyazı dosyaları, bir dereceye kadar videodan bağımsızdır ve oluşturuldukları video dosyalarından farklı video dosyalarıyla kullanılabilirler.
Bu, yazı tipi boyutlarının ve koordinatların nasıl yorumlanacağını kontrol eden ve yaygın olarak "betik çözünürlüğü" (script resolution) olarak bilinen sanal bir video çözünürlüğü kullanılarak elde edilir.
Ne yazık ki, altyazı formatının referans uygulamasındaki (VSFilter) bazı hatalar nedeniyle, betik çözünürlüğü gerçek video çözünürlüğüne eşit olmayan altyazıların işlenmesi (rendering) düzgün çalışmamaktadır.

Uyumsuz betik ve video çözünürlüklerinin davranışı kafa karıştırıcı olabileceğinden, karmaşık biçimlendirmeler yaparken bunları aynı tutmanızı öneririz.
Eğer farklı çözünürlüklerdeki birden fazla video için tek bir altyazı dosyası yayınlıyorsanız, tek bir dosyayı her video çözünürlüğüne dönüştürmek için [Çözünürlük Yeniden Örnekleyici]({{< relref "Resolution_Resampler" >}}) kullanılabilir.
Ancak, sadece basit biçimlendirilmiş altyazılar oluşturuyorsanız, normalde bu konuda endişelenmenize gerek yoktur.

______________________________________________________________________

Betik çözünürlüğünden etkilenen birkaç kategori vardır:

Mutlak koordinatlar (kenar boşlukları, `\pos`, `\move`, `\clip`, vektör çizimleri): tüm mutlak koordinatlar betik çözünürlüğü piksellerindedir ve mantıklı bir şekilde çalışır.

Yazı tipi boyutları: ASS'deki yazı tipi boyutu, betik çözünürlüğü piksellerindeki *satır yüksekliğidir*.
Bunun normal yazı tipi boyutu tanımı olmadığını ve genişliği hiç kullanmadığını unutmayın.
Sonuç olarak, betik çözünürlüğü, anamorfik videolar için altyazıların en boy oranını ayarlamak amacıyla kullanılamaz.

Kenarlık boyutları, gölge mesafesi ve bulanıklık gücü: bunlar betik çözünürlüğü veya video çözünürlüğü piksellerinde olabilir.
Hangisinin kullanılacağı, başlıktaki ScaledBorderAndShadow alanı tarafından kontrol edilir: eğer "yes" (evet) ise betik çözünürlüğü, "no" (hayır) ise video çözünürlüğü kullanılır.
Bunların betik çözünürlüğüne göre ölçeklendirilmesi her zaman etkinleştirilmelidir.

### Betik çözünürlüğünü değiştirme

Betik çözünürlüğü, [Özellikler]({{< relref "Properties" >}}) iletişim kutusundaki değer değiştirilerek veya [Çözünürlük Yeniden Örnekleyici]({{< relref "Resolution_Resampler" >}}) aracıyla betiği yeni bir çözünürlüğe yeniden örnekleyerek değiştirilebilir.
Hangisinin yapılacağı, çözünürlüğü neden değiştirmeniz gerektiğine bağlıdır.
Eğer şu anda herhangi bir nedenle yanlış çözünürlüğe ayarlanmış, biçimlendirilmemiş bir altyazı betiğiniz varsa, bunu [Özellikler]({{< relref "Properties" >}}) iletişim kutusunda değiştirin.
Eğer betik zaten biçimlendirilmişse ve şimdi onu farklı bir çözünürlükteki videoyla kullanmak istiyorsanız, [Çözünürlük Yeniden Örnekleyici]({{< relref "Resolution_Resampler" >}}) aracını kullanın.

### YCbCr Matrisi

Videonun içindeki bir renkle tam olarak eşleşmesi gereken altyazılar oluşturmadığınız sürece (örneğin ekranın bir kısmını vektör çizimiyle maskeliyorsanız) bunu tamamen görmezden gelebilirsiniz.

ASS'deki renkler BGR değerleri olarak belirtilir, ancak videolar normalde YCbCr olarak depolanır ve ikisi arasında birkaç olası dönüşüm vardır.
Bazı durumlarda altyazı işleyici, Aegisub'ın altyazı işleme performansıyla doğru bir şekilde eşleşebilmek için Aegisub tarafından hangi renk matrisinin kullanıldığını bilmelidir.
Bu, Aegisub'ın güncel sürümleri tarafından normalde otomatik olarak doğru ayarlanır, ancak 3.1 öncesi sürümlerle oluşturulmuş betiklerle çalışıyorsanız manuel olarak ayarlamanız gerekebilir.

### Otomatik çözünürlük değişikliği

Betik çözünürlüğünden farklı bir çözünürlüğe sahip bir video açtığınızda, Aegisub varsayılan olarak size ne yapmanız gerektiğini soracaktır.

Video ve betik aynı en boy oranına sahipse, aşağıdaki iletişim kutusunu alırsınız:

![çözünürlük-uyumsuzluğu](/img/3.2/resolution-mismatch.png#center)

"Resample script" (Betiği yeniden örnekle), altyazıları [Çözünürlük Yeniden Örnekleyici]({{< relref "Resolution_Resampler" >}}) kullanmışsınız gibi yeni videonun çözünürlüğüne yeniden örnekler ve az önce açtığınız video için önceden var olan altyazıları güncelliyorsanız genellikle istediğiniz şey budur.

"Set to video resolution" (Video çözünürlüğüne ayarla), betik çözünürlüğünü basitçe videonun çözünürlüğüne ayarlar.
Bu, yalnızca altyazılar aslında az önce açtığınız videoyla zaten eşleşiyorsa, ancak birisi daha önce betik çözünürlüğünü yanlış bir değere değiştirdiyse yapılacak doğru şeydir.

Cancel (İptal) veya ESC tuşuna basmak, betik çözünürlüğünü mevcut değerinde bırakır.
Altyazılar zaten nihai video çözünürlüğü için biçimlendirildikten sonra daha düşük çözünürlüklü bir ham (raw) video açıyorsanız bunu yapmak istersiniz.

______________________________________________________________________

Videonun en boy oranı betiğinkinden farklıysa, aşağıdaki iletişim kutusunu alırsınız:

![çözünürlük-uyumsuzluğu-ar](/img/3.2/resolution-mismatch-ar.png#center)

En boy oranının değişmiş olabileceği birkaç yaygın senaryo vardır:

- Yeni video anamorfiktir ancak betik önceden esnetilmiş bir video ile oluşturulmuştur (veya tam tersi).
  Bu durum tipik olarak 720x480'lik bir görüntünün oynatma sırasında 640x480 veya 853x480'e esnetildiği DVD'lerde gerçekleşir.
  Bu durumda, esneme anamorfik işleme ile iptal edileceğinden, altyazıları yeni en boy oranına göre esnetmek istersiniz.

- Orijinal video sadece içerik alanını içeriyordu ve yeni video üst ve alt kısımlara ya da sağ ve sol taraflara siyah kenarlıklar ekledi.
  Alternatif olarak, orijinal video pan-and-scan (tüm ekranı kaplayacak şekilde kırpılmış) bir sürümdü, yeni video ise görüntünün tamamını içeriyor.
  Bu durum için "add borders" (kenarlık ekle) seçeneğini seçin.

- Orijinal videoda siyah kenarlıklar vardı ve yenisinde yok ya da yeni video pan-and-scan.
  "remove borders" (kenarlıkları kaldır) seçeneğini seçin.