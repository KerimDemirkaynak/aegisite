---
title: Çeşitli API'ler
menu:
  docs:
    parent: lua-reference
weight: 6250
aliases:
  - /docs/latest/Automation/Lua/Miscellaneous_APIs/
---

Bu sayfa, **altyazılarla çalışırken yararlı olan çeşitli API'leri** belgelemektedir. Bunlar diğer ana kategorilerin hiçbirine net bir şekilde yerleştirilemeyen ve her türden ayrı bir kategori oluşturmayı gerektirmeyecek kadar az sayıda olan işlevlerdir.

## aegisub.cancel

Özet: `aegisub.cancel()`

Geçerli betiğin yürütülmesini derhal sonlandırır ve içinde yapılmış olan tüm değişiklikleri geri alır.

Bu işlev asla bir değer döndürmez.

## aegisub.text_extents

Özet: `width, height, descent, ext_lead = aegisub.text_extents(style, text)`

Sistem yazı tipi metriklerini elde eder ve **stil** kullanıldığında verilen **metnin** pikseller cinsinden oluşturulmuş boyutunu belirler.

`@style` (`table`)
: Altyazı arayüzü tarafından tanımlanan bir [stil tablosu]({{< relref "modules/karaskel.lua.md#style-table" >}}). Yazı tipi adı, boyutu, ağırlığı, stili, aralığı ve kodlaması metnin boyutunu belirlemek için kullanılır.

`@text` (`string`)
: Boyutlarının belirlenmesi gereken metin. Bu, satır sonları (`\n` veya `\r\n`) içermemeli ve hiçbir türde biçimlendirme kodu içermemelidir. Biçimlendirme kodları yorumlanmaz ve metin olarak olduğu gibi alınır.

`width` (`number`)
: Metnin piksel cinsinden genişliği. Bu değer tamsayı olmayabilir.

`height` (`number`)
: Metnin piksel cinsinden yüksekliği. Bu değer tamsayı olmayabilir.

`descent` (`number`)
: Yazı tipindeki alt uzantıların (descender) uzunluğu. Bu değer tamsayı olmayabilir.

`ext_lead` (`number`)
: Yazı tipi için harici satır aralığı. Bu değer tamsayı olmayabilir.

Bu işleve yalnızca satır sonu içermeyen düz metin dizeleri göndermelisiniz. Hiçbir türde biçimlendirme kodunu veya metin düzenini işleyemez. Daha ziyade, betik tarafından düzenlenebilecek daha uzun bir metnin parçalarının oluşturulmuş boyutlarını belirleyerek metin düzenleri oluşturmak için bir yardımcı olarak tasarlanmıştır.

## aegisub.gettext

Özet: `translation = aegisub.gettext(untranslated)`

Bir dizenin çevirisini alır. Bu, çoğunlukla yalnızca Aegisub ile birlikte gelen betikler için tasarlanmıştır (kendi çevirilerinizi eklemenizin bir yolu olmadığından), ancak Aegisub'da mevcut olan dizeleri kullanıyorsanız yararlı olabilir.

Paket halindeki makrolarda, dize çıkarıcısı (string extractor) adına bunun her zaman `tr` olarak takma adlandırıldığını unutmayın.

## Video hakkında bilgi alma

Automation 4 Lua, video kaynağının VFR veya CFR olup olduğunu dikkate almaya gerek kalmadan kare tabanlı zamanlama ile çalışmak üzere tasarlanmış iki işlev sunar.

Bu işlevlerin temel amacı, kare başına efektler üretebilmek, yani bir dizi ardışık karenin zaman damgalarını alabilmek ve bu karelerin her biri için bir nesnenin koordinatlarını, boyutlarını vb. hesaplayabilmektir.

Bu işlevleri kullanırken hatırlanması gereken bir şey, tek boyutlu bir zaman çizelgesi düşünüldüğünde, bir zaman damgasının zaman çizelgesindeki bir nokta olduğu, bir video karesinin ise zaman çizelgesinin başlangıç zamanından bitiş zamanına kadar olan bir aralığını kapsadığıdır. Bir karenin bitiş zamanı, bir sonrakinin başlangıç zamanıdır. Bir karenin başlangıç zamanı aralığa dahil edilirken, bitiş zamanı aralığın dışında tutulur.

### aegisub.frame_from_ms

Özet: `frame = aegisub.frame_from_ms(ms)`

**Milisaniye** cinsinden verilen mutlak bir zamanı bir **kare** numarasına dönüştürmek için yüklenmiş kare hızı verilerini kullanır.

`@ms` (`number`)
: Kare numarasını belirlemek için videonun başından itibaren mutlak zaman.

`frame` (`number`)
: Zamanın ms cinsinden karşılığı olan kare numarası veya kare hızı verisi yüklü değilse `nil`.

Eğer zaman, karenin ortasındaysa, verilen zamanı içeren kare numarasına **aşağı yuvarlanır**.

### aegisub.ms_from_frame

Özet: `ms = aegisub.ms_from_frame(frame)`

Videonun bir **kare** numarasını **milisaniye** cinsinden mutlak bir zamana dönüştürmek için yüklenmiş kare hızı verilerini kullanır.

`@frame` (`number`)
: Başlangıç zamanı alınacak kare.

`ms` (`number`)
: Kare içinde yer alan ilk tamsayı milisaniye zaman damgası veya kare hızı verisi yüklü değilse `nil`.

Karelerin başlangıç zamanları bir milisaniyeden daha iyi bir hassasiyete sahip olabileceğinden, bu işlev yukarı yuvarlama yapar ve kare içinde olduğu garanti edilen ilk tam milisaniyeyi döndürür.

### aegisub.video_size

Özet: `xres, yres, ar, artype = aegisub.video_size()`

Varsa, yüklenen videonun çözünürlüğü ve en-boy oranı hakkında bilgi alır.

`xres` (`number`)
: Videonun piksel cinsinden kodlanmış genişliği veya video yüklü değilse `nil`.

`yres` (`number`)
: Videonun piksel cinsinden kodlanmış yüksekliği veya video yüklü değilse `nil`.

`ar` (`number`)
: Özel görüntü en-boy oranı geçersiz kılması (override). `artype` 4 olmadıkça anlamsızdır.

`artype` (`number`)
: `artype`'ın alabileceği 5 değer vardır:

  - 0: Video kare piksellere sahiptir, yani PAR 1.00 ve DAR `xres`/`yres`'dir.
  - 1: Video 4:3'tür, yani DAR 1.33'tür.
  - 2: Video 16:9'dur, yani DAR 1.78'dir.
  - 3: Video 2.35 formatındadır, yani DAR 2.35'tir.
  - 4: DAR, `ar` dönüş değerinin içerdiği şeydir.

### aegisub.keyframes

Özet: `keyframes = aegisub.keyframes()`

Hangi video karelerinin anahtar kare (keyframe) olduğunun bir listesini alır.

`keyframes` (`table`)
: Her girdinin bir anahtar karenin kare numarası olduğu sıralı bir tablo. Eğer anahtar kare verisi yüklü değilse, tablo boş olacaktır.

## aegisub.decode_path

Özet: `path = aegisub.decode_path(encoded_path)`

Bir [yol belirticisi]({{< relref "Aegisub_path_specifiers" >}}) ile başlayan bir yolu mutlak bir yola dönüştürür.

`@encoded_path` (`string`)
: İsteğe bağlı olarak bir Aegisub [yol belirticisi]({{< relref "Aegisub_path_specifiers" >}}) ile başlayabilen bir dize.

`@path` (`string`)
: Eğer `encoded_path` geçerli bir [yol belirticisi]({{< relref "Aegisub_path_specifiers" >}}) ile başlıyorsa, mutlak bir yol. Eğer geçersiz bir yol belirticisi ile başlıyorsa (örneğin video açık değilken ?video kullanılmışsa), hiçbir şekilde yararlı olması muhtemel olmayan bir dize. Diğer tüm dizeler olduğu gibi aktarılır.

## aegisub.project_properties

Özet: `properties = aegisub.project_properties()`

Kullanıcının o anda hangi dosyaları açık tuttuğu hakkında bilgi içeren bir tablo alır. Bu tablonun tam içeriği kasten belgelenmemiştir ve uyarı yapılmaksızın değişebilir.