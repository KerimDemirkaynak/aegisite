---
title: İlerleme raporlama
menu:
  docs:
    parent: lua-reference
weight: 6230
aliases:
  - /docs/latest/Automation/Lua/Progress_reporting/
---

Bu fonksiyonlar, bir betik çalışırken GUI'ye çeşitli durum ve ilerleme bilgilerini raporlamak için kullanılır.

## İlerleme raporlama

Bir Automation 4 Lua betiği çalışırken her zaman bir ilerleme iletişim kutusu gösterilir. İçinde ne görüntüleneceğini kontrol etmek için bu fonksiyonları kullanabilirsiniz.

### aegisub.progress.set

Özet: `aegisub.progress.set(yüzde)`

İlerleme penceresindeki yüzde-tamamlandı çubuğunun konumunu ayarlar.

`yüzde` (`number`)
: 0 ile 100 arasında bir sayı.

### aegisub.progress.task

Özet: `aegisub.progress.task(mesaj, ...)`

İlerleme penceresinde, ilerleme çubuğunun altında bulunan ve betiğin o anda ne yaptığını gösteren küçük "görev" metnini ayarlar.

`mesaj` (`string`)
: Mesajı belirten bir format dizisi. Format dizileriyle ilgili ayrıntılar için Lua standart dizgi kütüphanesindeki `string.format` fonksiyonuna bakın.

`...`
: Format dizisi için parametreler.

### aegisub.progress.title

Özet: `aegisub.progress.title(başlık, ...)`

İlerleme penceresinin, ilerleme çubuğunun üzerinde görüntülenen büyük başlığını ayarlar. Bu metin normalde betik çalışırken değişmemelidir. Varsayılan olarak, çalışmakta olan makronun adıdır.

`başlık` (`string`)
: Başlığı belirten bir format dizisi. Format dizileriyle ilgili ayrıntılar için Lua standart dizgi kütüphanesindeki `string.format` fonksiyonuna bakın.

`...`
: Format dizisi için parametreler.

### aegisub.progress.is_cancelled

Özet: `iptal_edildi = aegisub.progress.is_cancelled()`

Kullanıcının İptal düğmesine tıklayıp tıklamadığını bildirir.

Bu fonksiyonu uzun işlemler sırasında düzenli olarak çağırmalısınız; eğer `true` (doğru) dönerse, tüm değişiklikleri geri almak ve betiğin yürütülmesini derhal sonlandırmak için [`aegisub.cancel()`]({{< relref "Miscellaneous_APIs#aegisubcancel" >}}) fonksiyonunu çağırın.

`iptal_edildi` (`boolean`)
: Kullanıcı İptal düğmesine tıklamadıysa `false` (yanlış), tıkladıysa `true` (doğru). Eğer `is_cancelled` değeri `true` dönerse, mevcut yürütme içindeki sonraki tüm çağrılar da `true` dönecektir.

## Hata ayıklama çıktısı

Automation 4 Lua'da betik hata ayıklaması için temel destek, ilerleme penceresine entegre edilmiş mesaj günlüğüne hata ayıklama mesajları gönderilerek sağlanır.

Bir betik hata ayıklama veya başka bir mesaj gösterirse, ilerleme penceresi betik çalışmayı bitirdikten sonra kullanıcı Kapat düğmesine tıklayana kadar açık kalır. Lütfen mesajlarınızı kullanıcının görmesinin gerçekten önemli olup olmadığını değerlendirin. Kullanıcıyla ilgisi olmayan bir şeyi görüntülemek için programın diğer girişlerini engellemek kötü bir deneyim yaratabilir.

### aegisub.debug.out

Özet:

- `aegisub.debug.out(mesaj, ...)`
- `aegisub.debug.out(seviye, mesaj, ...)`
- `aegisub.log(mesaj, ...)`
- `aegisub.log(seviye, mesaj, ...)`

Bu iki isim eş anlamlıdır; tercihinize göre herhangi birini kullanabilirsiniz.

İsteğe bağlı olarak belirli bir önem derecesi ile mesaj günlüğüne bir mesaj gönderir. Kullanıcı, Aegisub seçenekleri içinden gösterilecek en yüksek seviyeli mesajları kontrol edebilir.

`seviye` (`number`)
: Mesajın önem derecesi. Bu parametre isteğe bağlıdır. Eğer belirtmezseniz (tamamen atlarsanız), mesaj her zaman gösterilir.

`mesaj` (`string`)
: Mesajı belirten bir format dizisi. Format dizileriyle ilgili ayrıntılar için Lua standart dizgi kütüphanesindeki `string.format` fonksiyonuna bakın.

`...`
: Format dizisi için parametreler.

Aşağıdaki önem dereceleri önerilir:

0: "ciddi" (fatal)
: Çok kötü bir şey oldu ve betik devam edemiyor. 0 seviyeli mesajlar her zaman gösterilir. Aegisub'ın betiğinizi otomatik olarak sonlandırmadığını unutmayın. Eğer sonlandırmak istiyorsanız, sonrasında [`aegisub.cancel()`]({{< relref "Miscellaneous_APIs#aegisubcancel" >}}) fonksiyonunu çağırın.

1: "hata" (error)
: Gerçek bir hata oluştu, bu yüzden kurtarmaya çalışsanız bile kullanıcının bir şeylerin ters gitmesini beklemesi gerekir. Daha sonra ciddi bir hata oluşabilir.

2: "uyarı" (warning)
: Bir şeylerin yanlış olduğu görünüyor ve kullanıcı bunu bilmeli, çünkü bir şeylerin düzeltilmesi gerektiği anlamına gelebilir.

3: "ipucu" (hint)
: Kullanıcının işleri nasıl iyileştirebileceğine dair bir tavsiye veya daha sonra uyarı ya da hataya neden olabilecek durumlar hakkında bir ipucu.

4: "hata ayıklama" (debug)
: Değişken içeriklerinin dökümleri gibi, betikteki hataları düzeltmeye yardımcı olması amaçlanan bilgiler.

5: "izleme" (trace)
: Betiğin ne yaptığına dair son derece ayrıntılı bilgiler; örneğin yapılan her bir adım için çok sayıda değişken dökümü içeren mesajlar.