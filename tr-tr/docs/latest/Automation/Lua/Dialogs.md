---
title: İletişim Kutuları
menu:
  docs:
    parent: lua-reference
weight: 6240
aliases:
  - /docs/latest/Automation/Lua/Dialogs/
---

Bu fonksiyonlar, kullanıcının etkileşime girebileceği iletişim kutularını görüntülemek için kullanılır.

## İletişim kutusu görüntüleme fonksiyonları

### aegisub.dialog.display

Özet: `button, result_table = aegisub.dialog.display(dialog, buttons, button_ids)`

Bu fonksiyon kullanıcıya bir yapılandırma iletişim kutusu görüntüler ve kapanmasını bekler. Ardından kullanıcının iletişim kutusunu kabul edip etmediğini veya iptal edip etmediğini ve hangi değerlerin girildiğini döndürür.

`@dialog` (`table`)
: İletişim kutusunda bulunacak kontrolleri içeren bir [İletişim Kutusu Tanım tablosu]({{< relref "Dialogs#dialog-definition-table-format" >}}).

`@buttons` (`table`)
: İsteğe bağlı. İletişim kutusunda görünecek düğmeleri tanımlayan bir dizidir. Eğer bu kısım boş bırakılırsa, boşsa veya bir tablo değilse, standart Tamam ve İptal düğmeleri görünür.
  Bu tablodaki dizeler düğmelerin üzerindeki etiketler olarak ve fonksiyonun dönüş değerlerinde onları tanımlamak için kullanılır.

`@button_ids` (`table`)
: İsteğe bağlı. İletişim kutusundaki hangi düğmelerin hangi [platform düğme kimliklerine]({{< relref "Dialogs#dialog-button-ids" >}}) karşılık geldiğini belirten bir tablo; bu sayede kullanıcı Enter veya ESC tuşuna bastığında hangi düğmenin tetikleneceği belirlenebilir.

`button` (`boolean` veya `string`)
: Eğer özel düğmeler belirtilmediyse, bu değer Tamam'ın (true) veya İptal'in (false) tıklandığını belirten bir boolean değeridir. Eğer özel düğmeler belirtildiyse, bu değer kullanıcının tıkladığı düğmenin üzerindeki metindir. Özel düğmeler belirtilmiş olsa bile, kullanıcı hiçbir düğmeye basmadan iletişim kutusunu kapatırsa bu değer boolean false olabilir.

`result_table` (`table`)
: Kullanıcının iletişim kutusuna girdiği değerlere karşılık gelen [İletişim Kutusu Sonuç tablosu]({{< relref "Dialogs#dialog-result-table-format" >}}).

{{<example-box>}}

```lua
config = {
    {class="label", text="Frobulate sayısı", x=0, y=0},
    {class="intedit", name="times", value=20, x=0, y=1}
}
btn, result = aegisub.dialog.display(config,
        {"Frobulate", "Vazgeç"},
        {"ok"="Frobulate", "cancel"="Vazgeç"})
if btn then
    frobulate(result.times)
end
```

{{</example-box>}}

### aegisub.dialog.open

Özet: `file_name = aegisub.dialog.open(title, default_file, default_dir, wildcards, allow_multiple=false, must_exist=true)`

Kullanıcıdan bir dosya adı istemek için standart bir dosya açma iletişim kutusu açar. Seçilen dosya(lar)nın yolunu döndürür; kullanıcı iptal ederse nil değerini döner.

`@title` (`string`)
: İletişim kutusunun başlığı

`@default_file` (`string`)
: Önceden seçili olması için varsayılan dosya adı. Boş olabilir.

`@default_dir` (`string`)
: Açma iletişim kutusunda gösterilecek başlangıç dizini. Boşsa, son kullanılan dizin gösterilir.

`@wildcards` (`string`)
: Gösterilecek dosya filtreleri. Boşsa, makul bir varsayılan kullanılır.
  Örn: "Tüm Dosyalar (*.*)|*.*|XYZ dosyaları (*.xyz)|*.xyz"

`@allow_multiple` (`boolean`)
: Kullanıcının birden fazla dosya seçmesine izin verir. Bu true ise, kullanıcı tek bir dosya seçse bile tek bir dize yerine dosya adlarından oluşan bir tablo döndürülür.

`@must_exist` (`boolean`)
: Kullanıcının yalnızca gerçekten var olan dosyaları seçmesine izin verir.

`file_name` (`nil`, `string` veya `table`)
: Kullanıcı iptal ederse `nil`. `allow_multiple` false ise seçilen dosyanın yolunu içeren bir `string`, `allow_multiple` true ise seçilen tüm dosyaların yollarını içeren bir tablo döner.

{{<example-box>}}

```lua
filename = aegisub.dialog.open('Okunacak dosyayı seçin', '', '',
                               'Metin dosyaları (.txt)|*.txt', false, true)
if not filename then aegisub.cancel() end

file = io.open(filename, 'rb')
....
```

{{</example-box>}}

### aegisub.dialog.save

Özet: `file_name = aegisub.dialog.save(title, default_file, default_dir, wildcards, dont_prompt_for_overwrite=false)`

Kullanıcıdan bir dosya adı istemek için standart bir dosya kaydetme iletişim kutusu açar. Seçilen dosyanın yolunu döndürür; kullanıcı iptal ederse nil değerini döner.

`@title` (`string`)
: İletişim kutusunun başlığı

`@default_file` (`string`)
: Önceden seçili olması için varsayılan dosya adı. Boş olabilir.

`@default_dir` (`string`)
: Açma iletişim kutusunda gösterilecek başlangıç dizini. Boşsa, son kullanılan dizin gösterilir.

`@wildcards` (`string`)
: Gösterilecek dosya filtreleri. Boşsa, makul bir varsayılan kullanılır.
  Örn: "Tüm Dosyalar (*.*)|*.*|XYZ dosyaları (*.xyz)|*.xyz"

`@dont_prompt_for_overwrite` (`boolean`)
: Kullanıcı zaten var olan bir dosya adı seçerse, üzerine yazmak isteyip istemediğini onaylamasını istemez.

`file_name` (`nil` veya `string`)
: Kullanıcı iptal ederse `nil`, aksi takdirde seçilen dosyanın yolunu içeren bir `string` döner.

## Yapılandırma İletişim Kutusu arayüzü

Bu bölüm, `aegisub.dialog.display` fonksiyonuna aktarılan ve bu fonksiyondan alınan tabloları ve [dışa aktarma filtresi yapılandırma panelini]({{< relref "Registration#export-filter-configuration-panel-provider" >}}) açıklar.

Bu dosya, Automation 4'teki Yapılandırma İletişim Kutusu işlevselliği için kullanılan fonksiyonları ve veri yapılarını açıklar.

### İletişim Kutusu Kontrol tablosu formatı

Bir İletişim Kutusu Kontrol tablosu, bir yapılandırma iletişim kutusundaki tek bir kontrolü tanımlar; bu kontrol kullanıcıya bilgi görüntüleyebilir ve değiştirmesine izin verebilir.

Birçok farklı kontrol sınıfı vardır ve bir İletişim Kutusu Kontrol tablosunun içermesi gereken anahtarlar, kontrol sınıfına bağlıdır.

Tüm kontrol sınıfları için ortak anahtarlar:

`class` (`string`)
: Bu kontrolün hangi sınıfa ait olduğunu tanımlar. Şunlardan biri olmalıdır:

  - "label" (etiket),
  - "edit" (düzenleme), "intedit" (tam sayı düzenleme), "floatedit" (ondalık sayı düzenleme), "textbox" (metin kutusu),
  - "dropdown" (açılır menü),
  - "checkbox" (onay kutusu),
  - "color" (renk), "coloralpha" (renk ve alfa), "alpha" (alfa)

`x` (`number`)
`y` (`number`)
`width` (`number`)
`height` (`number`)
: Kontrolün iletişim kutusundaki konumunu ve boyutunu belirler. Bu değerler kontrolleri içeren bir ızgara oluşturmak için kullanılır. Hepsi tam sayı olmalıdır. Sol üst köşe `x`,`y`=0,0'dır.
  Genişlik veya yükseklikten herhangi biri sıfır veya daha küçük ayarlanırsa, bunun yerine bir olarak ayarlanır.

"label" dışındaki tüm sınıflar için tanımlı anahtarlar:

`hint` (`string`)
: Kontrolün üzerine gelindiğinde kullanıcıya araç ipucu olarak görüntülenen bir dize.

`name` (`string`)
: Kontrolü benzersiz şekilde tanımlayan bir isim. Bu ismin Lua'da tanımlayıcı olarak kolayca kullanılabilecek bir dize olması önerilir, çünkü kontrole girilen değere erişmek için kullanılacaktır.

Sadece "label" ve "checkbox" sınıfları için tanımlı anahtar:

`label` (`string`)
: Kontrol üzerinde kullanıcıya görüntülenen metin.

Sadece "edit" ve "textbox" sınıfları için tanımlı anahtar:

`text` (`string`)
: İletişim kutusu ilk görüntülendiğinde kontrolün içeriği.
  Kontrol "textbox" sınıfındaysa bu değer satır sonları içerebilir.

Sadece "intedit" ve "floatedit" sınıfları için tanımlı anahtarlar:

`value` (`number`)
: İletişim kutusu ilk görüntülendiğinde kontrolün içindeki değer. "intedit" sınıfı için, eğer bu bir tam sayı değilse kesilir.

`min` (`number` veya `nil`)
`max` (`number` veya `nil`)
: Bunlardan biri nil ise diğeri de nil olmalıdır (yani tanımlanmamış). Her ikisi de mevcutsa, kontrol, kullanıcının değeri güncellemek için tıklayabileceği bir sayı kutusu (spin button) kazanır. Kullanıcı `min` ve `max` arasındaki (dahil) aralığın dışındaki değerleri giremeyecektir.

Sadece "floatedit" sınıfı için tanımlı anahtar:

`step` (`number` veya `nil`)
: Sayı kutusuna tıklandığında değişim miktarını belirtir. Nil ise, `min` ve `max` ayarlanmış olsa bile sayı kutuları görüntülenmeyecektir (ancak kabul edilen değerler yine de sınırlandırılacaktır). Bunun `min` ve `max` ayarlanmasını gerektirmediğini unutmayın.

Sadece "dropdown" sınıfı için tanımlı anahtarlar:

`items` (`table`)
: Yalnızca dizeler içeren bir Dizi Tablosudur. Açılır kutuda kullanıcıya sunulan seçenekler için kullanılırlar.
  Dizi tablosundaki tüm dizeler benzersiz olmalıdır. (Benzersiz olmayan dizeleri birbirinden ayırt etmenin bir yolu yoktur.)

`value` (`string`)
: İletişim kutusu ilk görüntülendiğinde hangi öğenin seçili olduğunu belirler. Bu, belirtilen öğelerden biri değilse hiçbir öğe seçilmez. Büyük/küçük harf duyarlıdır.

Sadece "checkbox" sınıfı için tanımlı anahtar:

`value` (`boolean`)
: İletişim kutusu ilk görüntülendiğinde onay kutusunun işaretli olup olmadığını belirler.

Sadece "color", "coloralpha" ve "alpha" sınıfları için tanımlı anahtarlar:

`value` (`string`)
: VB veya HTML onaltılık (hexadecimal) formatında bir renk değeri.
  "color" sınıfı için bu 3 baytlık bir değer olmalıdır, örn. "#RRGGBB".
  "coloralpha" sınıfı için bu 4 baytlık bir değer olmalıdır, örn. "#RRGGBBAA".
  "alpha" sınıfı için bu bir baytlık bir değer olmalıdır, örn. "#AA".

### İletişim Kutusu Tanım tablosu formatı

İletişim Kutusu Tanım tablosu basitçe bir İletişim Kutusu Kontrol tabloları dizisidir.

Ancak, kontrollerin görsel sıralamasının tamamen kontrollerin "x", "y", "width" ve "height" değerleri tarafından belirlendiğini, ancak kontrollerin "sekmeli gezinme sırasının" (tab order) İletişim Kutusu Tanım tablosundaki sıralamalarına göre belirlendiğini unutmayın. Bunları eşleştirirseniz kullanıcılarınız size teşekkür edecektir.

### İletişim Kutusu Sonuç tablosu formatı

Bir İletişim Kutusu Sonuç tablosu, bir yapılandırma iletişim kutusundan gelen kullanıcı girişini içerir.

Bu tabloda anahtar olarak kontrollerin "`name`" özellikleri kullanılır.

Tablodaki her girişin değer türü, kontrolün sınıfına bağlıdır. Kontrol sınıfları türlerle şu şekilde eşleşir:

`label`: `nil`
: Kullanıcı bir etiketi değiştiremeyeceği için herhangi bir değer üretmezler.

`edit`, `textbox`: `string`
: Kutudaki metin girişi. **`textbox`** sınıfı bir kontrol durumunda satır sonları içerebilir.

`intedit`, `floatedit`: `number`
: Kontrole girilen sayı; sınıf tarafından (tam sayı veya ondalık sayı) ve min/max özellikleri tarafından belirlenen kısıtlamalar dahilinde olduğu garanti edilir.

`dropdown`: `string`
: Seçilen öğenin tam metni (büyük/küçük harf uyumlu).

`checkbox`: `boolean`
: Onay kutusunun işaretli durumu.

`color`, `coloralpha`, `alpha`: `string`
: **`value`** özelliğini ayarlamakla aynı şemayı takip eden bir VB renk dizesi.

İletişim kutusu sonuç tabloları tamamen iletişim kutusundan gelen çıktılardır. Bunları değiştirmek ve ardından iletişim kutusunu yeniden görüntülemek herhangi bir etki yaratmayacaktır.

### İletişim Kutusu düğme kimlikleri

Düğme kimlikleri için geçerli değerler:
ok
yes
save
apply
close
no
cancel
help
context_help

Düğme kimliklerinin birçok kombinasyonunun mantıklı olmadığını ve garip etkilere sahip olabileceğini unutmayın. Örneğin, hem `cancel` hem de `close` düğmelerine sahip olmak kötü bir fikirdir.

`cancel` kimliğine sahip düğmeler, ESC tuşuna basılmış gibi false değerini döndürür. `close` kimliğine sahip bir düğme, ESC tuşuna basıldığında iptal yerine o düğmenin tetiklenmesiyle sonuçlanır.

`ok`, `yes` ve `save` kimliğine sahip düğmeler, iletişim kutusu için varsayılan olumlu düğme olarak ayarlanır.

`help` kimliğine sahip düğmeler, OS X'te iletişim kutusunun sol tarafında daire içinde soru işareti olarak görüntülenir.