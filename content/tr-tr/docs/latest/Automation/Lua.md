---
title: Lua Referansı
menu:
  docs:
    parent: automation
    identifier: lua-reference
weight: 6200
aliases:
  - /docs/latest/Automation/Lua/
---

Automation 4 Lua betik motoru, [Lua betik dilinin](https://www.lua.org) 5.1 sürüm serisini temel alır.

Bu kılavuz, Lua dilinin kendisini veya Lua ile birlikte gelen standart kütüphaneleri değil, yalnızca Aegisub Automation 4 Lua arayüzü tarafından sağlanan ek işlevleri ve veri yapılarını ele alacaktır. Dilin kendisi ve standart kütüphaneleri hakkında ayrıntılı bilgi için lütfen [Lua 5.1 kılavuzuna](https://www.lua.org/manual/5.1/) bakın.

## Automation 4 Lua organizasyonuna genel bakış

En küçük geçerli Automation 4 Lua betiği boş bir dosyadır, ancak bu hiçbir ilginç işlem yapamaz.

Bir betiğin kendisi hakkında bilgi sağlamak için ayarlayabileceği bir dizi küresel değişken vardır. Bu bilgiler [Automation/Manager]({{< relref "./Manager" >}}) penceresinde görüntülenecektir: `script_name`, `script_description`, `script_author` ve `script_version`.

Automation 4 Lua, Automation 4'ün tanımlanmış iki "özelliğini" de uygular: Makro ve Dışa Aktarma Filtresi. Bir betik (bir dosya), bu özelliklerin her birinden sıfır, bir veya daha fazlasını tanımlayabilir. Örneğin, Karaoke Templater betiği bir makro ve bir dışa aktarma filtresi tanımlar.

Bir Automation 4 Lua betiği yüklendiğinde, en üst düzey kodu bir kez çalıştırılır. Değişken başlatmaları ve benzeri şeyleri en üst düzeye koyabilirsiniz, ancak genellikle yapacağınız şey, betik bilgisi küresel değişkenlerinden bazılarını tanımlamak, bazı modülleri içe aktarmak, betiğin işini yapan bazı işlevler yazmak ve ardından özellik kaydı işlevlerini çağırmaktır. Bu, **[Registration]({{< relref "./Lua/Registration" >}})** sayfasında açıklanmıştır. Betik yüklenirken dokunulması gereken tek `aegisub` nesnesi alanları `lua_automation_version` ve kayıt işlevleridir. Diğerlerinin çoğu sadece hiçbir şey yapmayacak ve `nil` döndürecektir.

Kullanıcı, Aegisub arayüzünden bir özelliği etkinleştirdiğinde (örneğin Automation menüsünden bir makro seçerek) kayıtlı betik işlevi çalıştırılır. İşleve aktarılan parametrelerden biri, betiğin değiştireceği altyazı verilerine birincil arayüz olan bir _altyazı nesnesidir_. Bir dereceye kadar, altyazı nesnesi tamsayı dizinli bir dizi gibi çalışır, ancak altyazı satırlarını eklemek, kaldırmak ve değiştirmek için bazı özel arayüzler sunar. Altyazı nesnesi, başlıklar, stil tanımları, diyalog satırları ve yorum satırları dahil olmak üzere altyazı dosyasındaki her satıra erişmenizi sağlar. Bu, **[Subtitle file interface]({{< relref "./Lua/Subtitle_file_interface" >}})** sayfasında açıklanmıştır.

Automation 4 Lua ayrıca, video kare zaman damgaları hakkında bilgi alma ve belirli bir stille oluşturulduğunda bir metnin ne kadar büyük olacağı gibi konularda temel API'de bir dizi yardımcı işlev sağlar.

Doğrudan Aegisub iç veri yapılarına bağlı olmayan, yani temiz Lua koduyla uygulanabilen çoğu şey, çekirdek API dışında [Lua modülleri]({{< relref "Modules" >}}) olarak uygulanmıştır. Sağlanan standart içerme dosyalarını kullanmadan Automation 4 Lua betikleri yazmak mümkün olsa da, en basit betikler dışındaki her şey için içerme dosyaları tarafından sağlanan işlevlerden bazılarına ihtiyaç duyacağınızı göreceksiniz.

## Automation 4 Lua çekirdek API'si

Automation 4 Lua, bu genel kategorilerde gruplanabilen çeşitli API'ler sağlar.

[Betik ve özellik kaydı]({{< relref "./Lua/Registration" >}})
: Bir betiğin hangi özellikleri sağladığının duyurulması ve diğer birkaç betik meta verisi ile ilgilenir.

[Altyazı dosyası arayüzü]({{< relref "./Lua/Subtitle_file_interface" >}})
: Altyazı verilerine erişmenin ve bunları değiştirmenin temel yolu olan _altyazı_ nesnesinin kullanımı ile ilgilenir.

[İlerleme raporlama ve hata ayıklama çıktısı]({{< relref "./Lua/Progress_reporting" >}})
: Bir betik çalışırken kullanıcıya geri bildirim sağlama, kullanıcıya ipuçları ve uyarılar verme ve hata ayıklama bilgilerini yazdırma.

[Diyalog kutuları görüntüleme ve kullanıcı girişi alma]({{< relref "./Lua/Dialogs" >}})
: Makro yürütme sırasında diyalog kutuları aracılığıyla kullanıcı girişi talep etme ve dışa aktarma filtreleri için bir yapılandırma arayüzü sağlama.

[Çeşitli API'ler]({{< relref "./Lua/Miscellaneous_APIs" >}})
: Örneğin metnin oluşturulmuş boyutunu alma ve video kare hızı bilgisi alma gibi işlemler için.