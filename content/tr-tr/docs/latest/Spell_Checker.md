---
title: Yazım Denetimi
menu:
  docs:
    parent: working-with-subtitles
weight: 3300
aliases:
  - /docs/latest/Spell_Checker/
---

Altyazı dosyalarınızın kalite kontrolüne yardımcı olmak için Aegisub, eksiksiz bir yazım denetimi özelliği sunar. OpenOffice.org'un MySpell tabanlı Hunspell kütüphanesini kullanır, bu da gelişmiş bir kelime işlemci programında bulabileceğiniz kadar iyi olduğu anlamına gelir. _Altyazılar_ menüsü -> _Yazım Denetimi_ yolundan ulaşılabilir. Ayrıca siz yazarken de yazımı denetler ve altyazı düzenleme kutusunun sağ tık menüsünden belirli bir ölçüde kontrol edilebilir (bkz. [altyazıları düzenleme]({{< relref "Editing_Subtitles" >}})).

### Yazım denetimi diyaloğu

![yazım_denetimi](/img/3.2/spell_checker.png#center)

Yazım denetimi diyaloğu, betiğinizde bulabildiği tüm yanlış yazılmış kelimelerin üzerinden geçer. Kutunun sol alt kısmındaki alan, yanlış yazılan kelime için önerileri görüntüler; sağ tarafta ise bir dizi düğme bulunur:

Açıklamaları Atla
: Yanlış yazılmış kelimeleri ararken açıklama satırlarını atlar. Açıklamalarınız çoğunlukla karaoke betikleri veya yeni bir dile çevirdiğiniz orijinal betik gibi şeyler olduğunda yararlıdır.

BÜYÜK HARFLİ kelimeleri yoksay
: Tamamı büyük harflerle yazılmış kelimeleri atlar. Altyazılarınızda çok sayıda uydurma kısaltma varsa ve hepsini sözlüğe eklemekle vakit kaybetmek istemiyorsanız kullanışlıdır.

Değiştir
: Bulunan yanlış yazılmış kelimeyi seçilen düzeltme ile değiştirir. Liste kutusuna çift tıklayarak da aynı işlemin yapılabileceğini unutmayın.

Tümünü Değiştir
: Bulunan yanlış yazılmış kelimenin _tüm betikteki_ tüm örneklerini seçilen düzeltme ile değiştirir.

Yoksay
: Yanlış yazılmış kelimenin _bu örneğini_ yoksayar, ancak bu yazım hatasının oluştuğu diğer yerlerde durmaya devam eder.

Tümünü Yoksay
: Bu kelimenin _tüm örneklerini_ bu yazım denetimi oturumu için yoksayar, ancak gelecekte tekrar kontrol edilmeye devam eder.

Sözlüğe ekle
: Bulunan kelimeyi sözlüğe ekler, böylece bir daha yanlış yazılmış olarak algılanmaz.

Sözlükten kaldır
: **Değiştir** alanındaki mevcut kelimeyi sözlükten kaldırır. Yalnızca **Sözlüğe ekle** işleviyle eklenmiş kelimeleri kaldırabilir, standart sözlükteki kelimeleri kaldıramaz.

Diyalog kutusunun en altında, yazım denetimi dilini seçmek için bir açılır kutu bulunur.

### Sözlükler

Aegisub'ın Windows sürümü bir ABD İngilizcesi sözlüğü ile gelir. Birçok diğer dil için yükleyiciler [web sitemizde](https://www.aegisub.org/downloads/#dictionaries) mevcuttur. Eğer diliniz için bir sözlük sağlamıyorsak, [Mozilla'nın sözlük setine](https://wiki.mozilla.org/L10n:Dictionaries) göz atın veya sadece Google'da "hunspell <i>\<dil></i> dictionary" şeklinde arama yapın. Paketlemek üzere ek sözlük gönderilerini memnuniyetle karşılıyoruz - geliştiricilerin hiçbirinin konuşmadığı diller için sözlük bulmak bazen zor olabiliyor.

Aegisub'ın OS X sürümü elimizdeki tüm sözlükleri içerir.

Linux'ta dağıtımınızın paket yöneticisi hunspell sözlüklerini bulundurmalıdır. [Sözlük yolunu]({{< relref "Options#interface" >}}) yüklendikleri konuma ayarlamanız gerekebilir; yaygın bir konum `/usr/share/hunspell` dizinidir.