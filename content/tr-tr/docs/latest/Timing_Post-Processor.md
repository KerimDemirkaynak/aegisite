---
title: Zamanlama Son İşlemcisi
menu:
  docs:
    parent: timing
weight: 5300
aliases:
  - /docs/latest/Timing_Post-Processor/
---

Zamanlama son işlemcisi, zamanlamayı çeşitli şekillerde otomatik olarak düzeltmek için oldukça kullanışlı bir araçtır.

## Genel Bakış

Ekran görüntüsünde gösterildiği gibi üç ana fonksiyon bulunmaktadır:

- Giriş (lead-in) ve/veya çıkış (lead-out) ekleme
- Birbirine yakın başlayan satırları, başlangıç ve/veya bitiş zamanlarını uzatarak veya kısaltarak sürekli hale getirme
- Satır başlangıçlarını/bitişlerini video anahtar karelerine (keyframes) hizalama (yalnızca video yüklüyse kullanılabilir)

![Zamanlama işlemcisi iletişim kutusu](/img/3.2/Dialog_timing_processor.png#center)

İşleme, iletişim kutusunda gösterildiği sırayla uygulanır. Yani önce giriş/çıkış süreleri eklenir, ardından bitişik satırlar kontrol edilir ve belirlenen eşik değerinden daha yakın olan satırlar sürekli hale getirilir, son olarak da satır başlangıç/bitişleri anahtar karelere hizalanır.

## Stil uygulaması

Bu alan hangi stillerin işleneceğini belirler; işlem yapmak istediğiniz tüm stilleri işaretleyin. Bu özellik, yalnızca diyalog satırlarını işleyip işaretleri ve/veya karaoke satırlarını olduğu gibi bırakmak için kullanışlıdır.

## Seçenekler

İşlemi yalnızca seçili satırlarla kısıtlamak için "Yalnızca seçime uygula" seçeneğini işaretleyin. Bu seçenek işaretlenmezse, dosyada seçili stillerle eşleşen tüm satırlar işlemden etkilenir.

## Giriş/Çıkış Süreleri (Lead-in/Lead-out)

Bu fonksiyon, bir satırın başlangıç/bitiş zamanlarını genişletir; bu işleme giriş ve çıkış ekleme denir. Son işlemci, belirlenen süreyi (milisaniye cinsinden) her satırın başlangıcına ve bitişine ekler. Kutuları gerektiği gibi işaretleyerek veya işaretini kaldırarak hem giriş hem çıkış, sadece biri veya hiçbiri eklenebilir. Giriş veya çıkış eklemek, halihazırda çakışmayan satırları asla çakıştırmaz.

## Bitişik altyazıları sürekli hale getirme

Bu fonksiyon, herhangi iki satırın başlangıç ve bitiş zamanlarının belirlenen eşikten (milisaniye cinsinden) daha yakın olup olmadığını kontrol eder. Eğer daha yakınsa, biri veya her ikisinin başlangıç ve/veya bitiş zamanı, sürekli olacak şekilde (yani biri, arada altyazısız kare kalmadan doğrudan diğerinin peşinden gelecek şekilde) hareket ettirilir.

*Sapma (Bias)* kaydırıcısı, satırların nasıl uzatılacağını belirler. Kaydırıcıyı tamamen sağa çekmek, birinci satırın bitiş zamanını ikinci satırın başlangıç zamanına kadar uzatır; bu sırada ikinci satıra hiç dokunulmaz. Sola çekmek ise, ikinci satırın başlangıç zamanını birinci satırın bitişine kadar geriye doğru uzatır; bu sırada birinci satıra dokunulmaz. Ortaya getirmek ise, her iki satırın zamanlarını eşit şekilde değiştirerek orta noktada birleşmelerini sağlar. Aradaki herhangi bir değer, satırların kaydırıcının konumuna göre "buluşmasını" sağlar. Örneğin, eşik 1000 ms ise ve kaydırıcı sağa doğru 3/4 oranındaysa (ekran görüntüsünde gösterildiği gibi), ilk satırın bitişi 750 ms uzatılırken, ikinci satırın başlangıcı 250 ms geriye doğru uzatılır.

*Bitişik altyazıları sürekli hale getirme* özelliğini çakışmaları gidermek için kullanırken, giriş veya çıkış eklemeyi etkinleştirmek istemeyebilirsiniz, çünkü bu işlem çakışma giderme işleminden önce uygulanır.

## Anahtar kareye hizalama (Keyframe snapping)

Anahtar kareye hizalama fonksiyonu, bir tür otomatik sahne zamanlayıcıdır. Üç fonksiyon arasındaki en kullanışlı olanı olabilir ancak anahtar karelere olan bağımlılığı nedeniyle sadece bir video veya anahtar kare dosyası yüklü olduğunda çalışır. [Video ile çalışma sayfasındaki anahtar kareler bölümüne]({{< relref "Video#keyframes" >}}) bakın.

Anahtar kareye hizalama fonksiyonu, satır başlangıç ve bitişlerinin en yakın anahtar kareye ne kadar yakın olduğuna bakar ve belirlenen eşik değerinden daha yakınlarsa, anahtar kareye uzatılır veya kısaltılır.

Dikkate alınması gereken dört eşik değeri vardır:

*Öncesinde başlat (Starts before)*
: Satır, bir anahtar kareden bu kadar milisaniye (dahil) veya daha kısa süre *önce* başlıyorsa, başlangıç zamanı ileri alınarak satırın tam anahtar karede başlaması sağlanır.

*Sonrasında başlat (Starts after)*
: Satır, bir anahtar kareden bu kadar milisaniye (dahil) veya daha kısa süre *sonra* başlıyorsa, başlangıç zamanı geri alınarak satırın tam anahtar karede başlaması sağlanır.

*Öncesinde bitir (Ends before)*
: Satır, bir anahtar kareden bu kadar milisaniye (dahil) veya daha kısa süre *önce* bitiyorsa, bitiş zamanı ileri alınarak satırın anahtar kareden önceki karede bitmesi sağlanır.

*Sonrasında bitir (Ends after)*
: Satır, bir anahtar kareden bu kadar milisaniye (dahil) veya daha kısa süre *sonra* bitiyorsa, bitiş zamanı geri alınarak satırın anahtar kareden önceki karede bitmesi sağlanır.

Bu özelliği kullanırken giriş/çıkış sürelerinizi unutmayın! *Öncesinde başlat* ve *Sonrasında bitir* eşikleriniz genellikle en az giriş ve çıkış süreleriniz kadar olmalıdır, aksi takdirde başlangıçta sahneye göre zamanlanmış satırlar kaymalara (bleed) neden olabilir.

Anahtar kareye hizalama özelliği ile yapabileceğiniz bir diğer şey de tek karelik kaymaları (one-frame bleeds) çok hızlı bir şekilde düzeltmektir. Eğer altyazı dosyanız bunlarla doluysa, tüm eşikleri 50'ye ayarlayın, giriş/çıkış eklemeyi ve bitişik satır hizalamayı devre dışı bırakın, diyalog stilinizi seçin ve "Uygula"ya basın. Sorun çözüldü.