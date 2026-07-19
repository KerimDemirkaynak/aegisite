---
title: Matematik ifadelerini kullanma
menu:
  docs:
    parent: automation-tutorials
weight: 6172
aliases:
  - /docs/latest/Automation/Karaoke_Templater/Tutorial_2/
---

[Bir önceki eğitimde]({{< relref "./Tutorial_1" >}}), basit karaoke efektleri yapmak için Karaoke Templater'ın temel özelliklerini nasıl kullanacağımızı gördük. Buradan devam ederek, geçen eğitimdeki temellerin üzerine eklemeler yapacağız.

{{<todo>}}ekran görüntüleri oluştur ve ekle {{</todo>}}

## Hazırlıklar

Daha önce olduğu gibi, zamanlanmış bir karaokeye ve efektleri önizlemek için bir videoya ihtiyacınız olacak. Burada bununla ilgili başka detaya girmeyeceğim.

## Solma (fadeout) ekleme

Özetlemek gerekirse, işte geçen eğitimin sonundaki efekt:

```ass
{\r\k$kdur\t($start,$end,\1c&H00FF00&)\t($start,$mid,\fscy120)\t($mid,$end,\fscy100)}
```

Şimdi buna bir solma (fadeout) efekti ekleyeceğiz; her hece söylenirken değil, söylendikten *sonra* solacak. Bunu yapmak için biraz matematik kullanmamız gerekecek: Solmayı `$end` zamanında başlatıp `$end+200` zamanına kadar, yani heceden sonra 200 milisaniye boyunca devam ettireceğiz.

Şablonu şu şekilde değiştirin:

```ass
{\r\k$kdur\t($start,$end,\1c&H00FF00&)\t($start,$mid,\fscy120)\t($mid,$end,\fscy100)\t($end,!$end+200!,\alpha&HFF&)}
```

Ardından şablonları tekrar uygulamayı deneyin. Eski efektin her zamanki gibi gerçekleştiğini, ancak bu sefer sonrasında her hecenin solduğunu görmelisiniz.

Bunun sihirli kısmı, buradaki ünlem işaretleridir: `!$end+200!`

Bunun gibi bir çift ünlem işaretine sahip olduğunuzda, aralarındaki her şey bir *ifade* olarak kabul edilir (aslında çok küçük bir Lua programıdır, ancak şimdilik bunu dert etmeyin). Burada, hecenin bitiş zamanını alıp ona 200 ekleyerek yeni bir sayı elde etmek için bir ifade kullanıyoruz. Sonuç olarak, `\t` solma efekti `$end` anından başlayıp 200 milisaniye sonrasına kadar sürer.

## Büyüme/küçülme efektine ince ayar yapma

Belki büyüme-küçülme efektinin tam ortada geçiş yaparak biraz tuhaf göründüğünü düşünüyorsunuzdur. Daha erken maksimum yüksekliğe ulaşması ve normale dönmek için daha fazla zaman harcaması daha iyi görünebilir. Pekala, bu değiştirilebilir:

```ass
{\r\k$kdur\t($start,$end,\1c&H00FF00&)\t($start,!$start+$dur*0.3!,\fscy120)\t(!$start+$dur*0.3!,$end,\fscy100)}
```

Bununla birlikte, büyüme kısmı hece süresinin sadece ilk onda üçünü, küçülme ise geri kalanını alacaktır. Burada yeni bir değişken kullandık: `$dur`. Bu, `$kdur` değişkeninin santisaniye cinsinden süresi olması gibi, milisaniye cinsinden hece süresidir. (Aslında burada `$kdur` değerini de kullanıp 0.3 yerine 3 ile çarpabilirdik.)

Satırı daha kısa ve okunması daha kolay hale getirmek için buradan solma efektini çıkardığımı unutmayın. İsterseniz onu geri ekleyebilirsiniz.

Umarım bu eğitim, neler yapabileceğiniz konusunda size daha fazla fikir vermiştir. [Bir sonraki eğitimde](#), birden fazla şablon kullanarak efekte başka bir katman ekleyeceğiz!