---
title: Çözünürlük Yeniden Örnekleyici
menu:
  docs:
    parent: typesetting
weight: 4700
aliases:
  - /docs/latest/Resolution_Resampler/
---

Çözünürlük Yeniden Örnekleyici (Resolution Resampler), etkilenen tüm etiketleri dönüştürürken [betik çözünürlüğünü]({{< relref "Script_Resolution" >}}) değiştirmek için tasarlanmış yerleşik bir araçtır, böylece sonuç aynı görünür. Ayrıca tüm kenar boşluklarını (ve mutlak konumları) belirli bir değerle kaydırabilir. Kullanım alanları arasında farklı çözünürlüklere sahip iki betiği birleştirme, 4:3 bir video için hazırlanmış bir betiği 16:9 eşdeğerine dönüştürme ve 1:1 ile anamorfik piksel formatları arasında geçiş yapma yer alır.

## Genel Bakış

![çözünürlük yeniden örnekleyici](/img/3.2/resolution_resampler.png#center)

Çözünürlük yeniden örnekleyicinin üç ana bölümü vardır: kaynak çözünürlüğü, hedef çözünürlüğü ve kaynak ile hedefin farklı en-boy oranlarına sahip olması durumunda ne yapılacağı.

Varsayılan olarak, kaynak çözünürlüğü mevcut betik özelliklerine, hedef çözünürlüğü ise videonun özelliklerine ayarlanır; bu genellikle istediğiniz durumdur. Kaynak ayarlarını değiştirmek genellikle yalnızca hatalı yapılan önceki yeniden örneklemeleri veya yanlış dizilmiş betikleri düzeltmek için yararlıdır.

SD çözünürlüklerinden HD çözünürlüklerine yeniden örnekleme yapıyorsanız, muhtemelen YCbCr matrisini TV.601'den TV.709'a dönüştürmek isteyeceksiniz; HD'den SD'ye dönüştürürken ise bunun tam tersini yapmalısınız.

Yeni çözünürlük ve eski çözünürlük aynı en-boy oranına sahip değilse, dört seçeneğiniz vardır:

1. Altyazıları yeni en-boy oranına esnetin.
   Bu, çözünürlüklerden birinin veya her ikisinin anamorfik olduğu ve aslında aynı görüntüyü temsil ettiği durumlar içindir.
1. Eski videoyu yeni video içinde ortalamak için gerekli kenar boşluklarını otomatik olarak ekleyin.
   Yeni videonuzda siyah kenarlıklar varsa veya eski videodan daha geniş bir görüntü alanı gösteriyorsa bunu kullanın.
1. Eski videoyu yeni video içinde ortalamak için gerekli kenar boşluklarını otomatik olarak kaldırın.
   Kaynak videoda siyah kenarlıklar varsa ve yeni videonuzda yoksa bunu kullanın.
1. Tüm satırları kaydırmak için kenar boşluklarını manuel olarak ayarlayın.
   Kenar boşluklarının yeniden ölçeklendirmeden sonra değil, *önce* eklendiğine dikkat edin.

## Örnekler

### 4:3 SD'den 16:9 HD'ye

Örneğin, 640x480 bir video için hazırlanmış altyazılarınız varsa ve aynı altyazıları 1280x720 bir videoya (geniş ekran olduğundan, sol ve sağ kenarlarda daha fazla video gösteren veya siyah kenarlıkları olan) uygulamak istiyorsanız, yeniden örnekleyiciyi yukarıdaki ekran görüntüsünde gösterilen ayarlara getirirsiniz.

### Anamorfik 720x480'den 640x480'e

Bunun için kaynak çözünürlüğünü 720x480, hedef çözünürlüğünü 640x480 olarak ayarlar ve en-boy oranı işleme seçeneği olarak "Esnet" (Stretch) ayarını seçersiniz.