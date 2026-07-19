---
title: Basit bir örnek
menu:
  docs:
    parent: automation-tutorials
weight: 6171
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Tutorial_1/
---

[Karaoke efektleri]({{< relref "../../Glossary/Karaoke_effect" >}}) oluşturmak için Karaoke Templater kullanımına dair ilk eğitime hoş geldiniz. Basit bir şeyle başlayıp seri boyunca daha gelişmiş efektlere doğru devam edeceğiz.

## Karaoke Templater'ı Bulma

Karaoke Templater'ı iki farklı şekilde çalıştırabilirsiniz. Şimdilik bunlardan sadece birine odaklanacağız.

Aegisub'daki Automation (Otomasyon) menüsünün altına bakın.

![Automation-menu-kara-templater-gray](/img/3.2/Automation-menu-kara-templater-gray.png)

_Apply karaoke template_ (Karaoke şablonunu uygula) adlı seçeneği görmelisiniz, ancak bu seçenek şu an devre dışı olacaktır. Bu eğitimler boyunca yazacağımız "şablonları" kullanmak için seçeceğiniz şey budur. Şu anda herhangi bir şablon girmediğiniz için devre dışıdır. Buna birazdan geleceğiz.

Eğer _Apply karaoke template_ seçeneğine sahip değilseniz, Aegisub kurulumunuz eksik veya hasarlıdır. Bu durumda Karaoke Templater'ı kullanabilmek için kurulumunuzu onarmanız gerekir.

Ancak öncelikle emin olmanız gereken başka bir şey daha var.

## Zamanlanmış karaoke elde etme

Karaoke Templater sizin için birçok şey yapabilir, ancak şarkınızın sözlerini veya bunların müzikle nasıl senkronize edildiğini tahmin edemez. Şarkı sözlerini kendiniz zamanlamalı ya da bir başkasına yaptırmalısınız. Karaoke zamanlamasının nasıl yapılacağını [Karaoke_Timing_Tutorial]({{< relref "Karaoke_Timing_Tutorial" >}}) kısmından öğrenebilirsiniz.

Temel karaoke zamanlamasına (\\k zamanlaması) sahip olan ancak başka özel efekt içermeyen şarkı sözlerine _zamanlanmış karaoke_ diyeceğiz. Karaoke'ye bir efekt uygulandığında buna _stilli karaoke_ diyeceğiz.

Eğer üzerinde çalışacak bir şarkınız yoksa, işte bir şarkıdan iki satır. Bunları tarayıcınızdan seçebilir, _Düzen_→_Kopyala_ diyebilir, ardından Aegisub'a gidip _Düzen_→_Yapıştır_ diyerek Aegisub'a aktarabilirsiniz.

```ass
Dialogue: 0,0:00:01.85,0:00:09.06,Default,,0000,0000,0000,,{\k97}shi{\k41}ta{\k0} {\k20}no{\k10} {\k30}u{\k80}e{\k53} {\k23}a{\k21}ma{\k39}ku{\k7}  {\k24}to{\k24}ke{\k31}ru{\k0} {\k37}wa{\k23}ta{\k92}gu{\k69}mo
Dialogue: 0,0:00:09.28,0:00:16.21,Default,,0000,0000,0000,,{\k79}ki{\k61}su{\k0} {\k9}o{\k0} {\k37}shi{\k98}te{\k40}  {\k23}ku{\k25}ro{\k40}i{\k0} {\k28}tsu{\k19}ba{\k51}sa{\k0} {\k11}no{\k0} {\k34}shi{\k138}ta
```

Her iki durumda da artık zamanlanmış karaoke sözleriniz var, yani başlayabiliriz.

### Bir video yükleyin

Herhangi bir ses yüklemenize gerek yok, ancak açık bir videonuzun olması iyi bir fikir olabilir. Kullanabileceğiniz herhangi bir video dosyanız yoksa, _Video_→_Use dummy video_ (Boş video kullan) seçeneğini seçin ve sadece OK'e basın. Alacağınız video çok ilginç olmayacaktır ancak altyazıların ve oluşturduğumuz efektin nasıl görüneceğini size gösterecektir.

## _k-replacer_ stili bir şablon yazma

Artık her şeyi ayarladığımıza göre asıl şablonu oluşturma zamanı. Öncelikle, onu nasıl ekleyeceğinizi görelim. Her bir parçanın ne anlama geldiğine dair açıklamalar bunu takip edecektir.

1. Dosyadaki ilk altyazı satırını seçin.
1. Yeni bir satır elde etmek için _Subtitles_→_Insert Lines_→_Before Current_ (Altyazılar→Satır Ekle→Mevcut Satırdan Önce) yolunu izleyin. Bu bizim karaoke şablon satırımız olacak. İlk sırada olması _gerekmez_, ancak genellikle kendi takibinizi yapmak için daha kolaydır.
1. Yeni oluşturulan satırın, zamanlanmış karaokenizle aynı _style_ (stil) değerine sahip olduğundan emin olun.
1. Yeni satır için _Comment_ (Yorum) onay kutusuna tıklayın. Altyazı ızgarasında rengi değişmelidir.
1. _Effect_ (Efekt) alanını bulun, _Style_ ve _Actor_ alanlarının sağ tarafındadır. İçine "`template line`" metnini yazın. (Tırnak işaretleri olmadan!) Effect alanını kaydetmek için klavyenizdeki _Enter_ tuşuna basın.
1. Son olarak, şablon satırınızın ana metni için şu metni girin. Yine _Enter_ ile bitirin: `{\r\t($start,$mid,\fscy120)\t($mid,$end,\fscy100)}`

{{<todo>}}Adımlardan sonra nasıl görünmesi gerektiğine dair bir ekran görüntüsü ekleyin. {{</todo>}}

Şimdi _Automation_ menüsüne tekrar bakın. Şablon satırını doğru bir şekilde oluşturduysanız, _Apply karaoke template_ artık kullanılabilir olacaktır. Değilse, yukarıdaki adımları tekrar gözden geçirin.

_Apply karaoke templates_ (Karaoke şablonlarını uygula) seçeneğini seçin ve Karaoke Templater'ın işini yapmasını izleyin.

{{<todo>}}Başka bir ekran görüntüsü, bu sefer şablon uygulandıktan sonra. {{</todo>}}

Eğer bir video açıksa, efekti şu an Aegisub içinde görüntüleyebilirsiniz.

Ayrıca şablon satırının yerinde bırakıldığına, zamanlanmış karaokenin ise yorum satırlarına dönüştürüldüğüne ve Effect alanlarına _karaoke_ değerinin yazıldığına dikkat edin. Karaoke Templater, zamanlanmış karaokenizi stilli karaoke içinde korur, böylece onu kaybetmezsiniz. Ancak başka bir işlevi daha vardır...

## Efekti biraz genişletme

Yukarıdakinden devam ederek şimdi şunu deneyin:

1. Şablon satırının metnini şu şekilde değiştirin: `{\r\k$kdur\t($start,$end,\1c&H00FF00&)\t($start,$mid,\fscy120)\t($mid,$end,\fscy100)}`
1. Şablonları tekrar uygulayın

{{<todo>}}Daha fazla ekran görüntüsü {{</todo>}}

Karaoke Templater, yorum satırı haline getirilmiş zamanlanmış karaokeyi yeniden kullandı ve stilli karaokeyi yeni efekte uyacak şekilde değiştirdi. Ayrıca yorum satırı halindeki zamanlanmış karaokeyi değiştirmeyi ve şablonları tekrar uygulamayı da deneyebilirsiniz.

Bu şekilde, efektiniz üzerinde kademeli olarak çalışabilir ve ilerledikçe önizlemesini görebilirsiniz.

## Peki tüm bunlar ne anlama geliyor?

Eğitimin bu ilk bölümünü bitirmek için, her bir parçanın ne anlama geldiğine bakalım. Bu her şeyin tam açıklaması değildir, ancak şimdilik fazlasıyla yeterli olacaktır.

- _Şablon satırları (Template lines)_, altyazı dosyasında özel bir şekilde işaretlenmiş satırlardır. Her zaman Yorum satırı olmaları ve Effect alanındaki ilk kelimenin `template` olması gerekir.
- Birkaç çeşit şablon satırı vardır. Bu eğitimde sadece birini kullandık; bu şablon satırı türüne veya _şablon sınıfına_, _satır şablonu (line template)_ denir. Evet, biraz kafa karıştırıcı olabilir. Buna böyle denmesinin sebebi, zamanlanmış bir karaoke satırından bir satır stilli karaoke oluşturmasıdır. Bir şablon satırının Effect alanındaki ikinci kelime, hangi şablon sınıfı olduğunu belirtir. Satır şablonları için bu `line` değeridir.
- Yani, Effect alanındaki `template line` metni, bunun _line sınıfından_ bir _şablon satırı_ olduğu anlamına gelir.

<!-- -->

- Bir şablon, yalnızca şablon satırı ile aynı Style değerine sahip olan zamanlanmış karaoke satırlarında bir işlem yapar.

<!-- -->

- Karaoke Templater tarafından oluşturulan tüm stilli karaokeler, Effect alanında `fx` ibaresine sahiptir. Bu, şablonlar tekrar uygulandığında, bu satırın değiştirilmesi gerektiğini Karaoke Templater'a hatırlatmak için kullanılır.

<!-- -->

- Bir şablon satırı için ana metne _şablon metni (template text)_ denir. _line_ şablonlarında, her \\k etiketi şablon metni ile değiştirilir.
- Şablon metni çeşitli _değişkenler_ kullanabilir. Bunlar `$start`, `$end`, `$mid` ve `$kdur` gibi dolar işaretiyle başlayan kısa kelimelerdir. Değişkenler, değiştirilen her hece için sakladıkları bilgilerle değiştirilir.
  - `$start`, hecenin başlama zamanı ile değiştirilir. Bu, satırın başlangıcından itibaren milisaniye cinsindendir; yani \\t, \\move ve \\fade etiketlerine koymak için uygun bir zaman kodudur.
  - Benzer şekilde, `$end` hecenin bitiş zamanıdır, yine milisaniye cinsinden.
  - Biraz daha özel olan `$mid`, hecenin _orta zamanıdır_, yani `$start` ile `$end` arasındaki tam orta nokta. Burada, her heceyi süresinin ilk yarısında daha uzun, ikinci yarısında normal yüksekliğine getirmek için kullandık. Yine milisaniye cinsinden.
  - `$kdur` değişkeni ise santisaniye cinsindendir. Bu, \\k etiketindeki orijinal zamandır ve neredeyse sadece burada yaptığımız gibi bir \\k etiketine geri koymak için kullanışlıdır.

Bu bilgiyle, zaten pek çok efekt yaratabiliyor olmalısınız. Ayrıca [ASS geçersiz kılma etiketleri]({{< relref "ASS_Tags" >}}) sayfasını da incelemek isteyebilirsiniz.

Ayrıca değişkenlerle matematiksel işlemler yaparak nasıl daha fazla çeşitlilik elde edeceğimize bakacağımız [bir sonraki eğitime devam edebilirsiniz]({{< relref "./Tutorial_2" >}}).