---
title: Zaman kaydırma
menu:
  docs:
    parent: timing
weight: 5200
aliases:
  - /docs/latest/Shift_Times/
---

**Zaman kaydırma** aracı, zaman damgaları için bir toplu işlemcidir; birçok altyazı satırının başlangıç/bitiş zaman damgalarını aynı anda çeşitli şekillerde ayarlar. _Zamanlama (Timing)_ -> _Zaman kaydırma (Shift Times)_ altında bulunur.

Şu şekilde görünür:

![zaman kaydırma](/img/3.2/shift_times.png#center)

Pencerenin sol kısmı seçenekleri içerir.

### Kaydırma miktarı

Bu kontroller, her zaman damgasının hangi yönde ve ne kadar değiştirileceğine karar verir.

Zaman
: Her zaman damgasını saat:dakika:saniye.santisaniye cinsinden ne kadar ayarlamak istediğiniz.

Kareler
: Eğer video yüklüyse, ayarlama süresini bunun yerine kare sayısı olarak belirtebilirsiniz. Sıfır kare kaydırmanın, herhangi bir kaydırma yapmadan zaman damgalarını kare zamanlarına sabitleyeceğini unutmayın.

İleri veya Geri
: Zaman damgalarının hangi yöne doğru ayarlanacağını kontrol eder.

### Etkilenecekler

Bu kontroller, hangi satırların işleneceğine karar verir.

Tüm satırlar
: Zaman kaydırmayı betikteki tüm satırlara uygular.

Seçili satırlar
: Zaman kaydırmayı yalnızca seçili satırlara uygular.

Seçimden itibaren
: Zaman kaydırmayı, seçilen ilk satıra ve (ızgaradaki) altındaki tüm satırlara uygular.

### Zamanlar

Bu kontroller, hangi zaman damgalarının işleneceğine karar verir.

Başlangıç ve Bitiş zamanları
: Etkilenen satırların hem başlangıç hem de bitiş zamanları verilen miktarda değiştirilir.

Sadece Başlangıç zamanları
: Sadece etkilenen satırların başlangıç zamanları değiştirilir. Bunun, satırları (geriye doğru kaydırırsanız) daha uzun veya (ileri doğru kaydırırsanız) daha kısa hale getireceğini ve hatta sıfır süreli yapabileceğini unutmayın.

Sadece Bitiş zamanları
: Sadece etkilenen satırların bitiş zamanları değiştirilir. Bunun, satırları (ileri doğru kaydırırsanız) daha uzun veya (geriye doğru kaydırırsanız) daha kısa hale getireceğini ve hatta sıfır süreli yapabileceğini unutmayın.

Bir satırın başlangıç veya bitiş zaman damgası negatif olacak şekilde kaydırılırsa, o zaman damgasının sıfırlandığına dikkat edin. Bu, betikteki en son zaman damgasından daha uzun bir süre geriye doğru kaydırılarak, tüm betikteki zamanlamaları temizlemek için kullanılabilir.

### Geçmişten yükle

Bu, kaydırma geçmişini temizlediğinizden (temizle butonu ile) bu yana yaptığınız tüm zaman kaydırma işlemlerinin bir geçmişidir. Biçim, virgülle ayrılmış bir dizi alandır. Alanlar şunlardır:

- Betiğin dosya adı (örneğin: "ornek.ass")
- Kaydırma miktarı ve yönü (örneğin: "0:00:05.00 ileri")
- Hangi zamanların etkilendiği; başlangıç için "s", bitiş için "e", her ikisi için "s+e"
- Hangi satırların etkilendiği; seçimler için "sel start-end", tüm satırlar için "all" (örneğin: "sel 1-40")

Geçmiş kaydından ayarları yüklemek için üzerine çift tıklamanız yeterlidir.