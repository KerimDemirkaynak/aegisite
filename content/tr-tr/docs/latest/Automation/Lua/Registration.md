---
title: Kayıt
menu:
  docs:
    parent: lua-reference
weight: 6210
aliases:
  - /docs/latest/Automation/Lua/Registration/
---

**Kayıt**, [Automation 4 Lua]({{< relref "Lua" >}}) betiğinizi Aegisub'a sunmayı, hakkında bilgi sağlamayı ve sağladığı _özellikleri_ kaydetmeyi kapsar.

## Özelliklerin açıklanması

Automation 4'teki temel kavramlardan biri _özellik_ (feature) kavramıdır. Özellik, bir betiğin, kullanıcının eylemine yanıt olarak Aegisub'ın geri çağırabilmesi için kullanıma sunduğu bir şeydir.

Bir özellik, basit bir geri çağırma (callback) değildir. Genellikle birkaç geri çağırma işlevinden oluşan bir küme ve bunların kullanıcı arayüzünde (GUI) nasıl sunulması gerektiğine dair bazı bilgilerdir.

Özelliklerden biri **makrodur**. Makro, Otomasyon menüsünde bir öğe olarak sunulur. Bir makronun adı (menüde görünen başlık), açıklaması (menü öğesinin üzerine gelindiğinde durum çubuğunda gösterilen metin), bir işleme işlevi (kullanıcı menü öğesini seçtiğinde çağrılan işlev) ve isteğe bağlı bir doğrulama işlevi (makronun mevcut durumda herhangi bir iş yapıp yapamayacağını belirleyen) vardır.

Bir diğer özellik ise **dışa aktarma filtresidir** (export filter). Dışa aktarma filtresi, [Dışa Aktar]({{< relref "Exporting" >}}) iletişim kutusunda sunulur ve bir dışa aktarma işlemi sırasında uygulanabilir. Dışa aktarma filtrelerinin de bir adı, açıklaması, işleme işlevi ve ardından isteğe bağlı bir yapılandırma paneli sağlayıcısı vardır. Yapılandırma paneli sağlayıcısı, dışa aktarma filtresi etkinleştirildiğinde Dışa Aktar iletişim kutusunda görüntülenecek bir yapılandırma iletişim kutusu tanımlama yapısı döndüren bir işlevdir. Yapılandırma paneline girilen ayarlar, çalıştırıldığında işleme işlevine aktarılır.

## Betik bilgisi genel değişkenleri

Bir betik, Aegisub'a betik hakkında meta veriler sağlamak için birkaç genel değişken belirleyebilir. Bu değişkenlerle verilen bilgiler [Otomasyon Yöneticisi]({{< relref "../Manager" >}}) iletişim kutusunda ve Betik Bilgisi iletişim kutusunda görüntülenir.

- **script_name** (string) - Betiğin adı. Kısa olmalıdır.
- **script_description** (string) - Betiğin amacının açıklaması. Çok uzun olmamalıdır.
- **script_version** (string veya number) - Betiğin sürüm numarası/adı. Bu serbest biçimlidir; buna özel bir anlam yüklenmemiştir.
- **script_author** (string) - Betik için yazar bilgileri.

Bunların tümü isteğe bağlıdır; bir betiğin bunların hiçbirini sağlaması gerekmez. Eğer betik adı verilmezse, görüntüleme amaçlı olarak dosya adı kullanılır.

## Kayıt işlevleri

Kayıt işlevleri, bir özelliği Aegisub için kullanılabilir hale getirmek amacıyla çağırabileceğiniz, Automation 4 Lua tarafından sağlanan işlevlerdir. Bunları genellikle betiğinizin en alt seviyesinde, en sonda çağırırsınız.

### aegisub.register_macro

Özet: `aegisub.register_macro(name, description, processing_function, validation_function, is_active_function)`

Bir makro özelliği kaydeder.

- **name** (string) - Otomasyon menüsünde görüntülenen ad. Çok kısa olmalı, üç kelime veya daha az olmaya çalışılmalı ve emir kipinde olmalıdır.

  Eğer ad içerisinde eğik çizgi (/) kullanılmışsa, ad eğik çizgiden bölünecek ve eğik çizgiden önceki kısım, makronun yerleştirileceği alt menünün adı olarak kullanılacaktır. Örneğin, "Foo/Bar" adlı bir makro ve "Foo/Baz" adlı bir makro kaydederseniz, otomasyon menüsü "Bar" ve "Baz" girişlerini içeren "Foo" adlı bir alt menüye sahip olacaktır.

  Menüler, işletim sisteminin desteklediği derinliğe kadar iç içe geçirilebilir, ancak bir seviyeden daha derine inmek iyi bir fikir olmayabilir.

- **description** (string) - Kullanıcı fareyi menü öğesinin üzerine getirdiğinde durum çubuğunda görüntülenen açıklama. Bu, makronun ne yaptığına dair özlü bir açıklama olmalıdır. En fazla 60 karakter tutmaya çalışın.

- **processing_function** (function) - Kullanıcı menü öğesini seçtiğinde çağrılan işlev. Bu, [makro işleme işlevi API'sine]({{< relref "Registration#macro-processing-function" >}}) sahip bir işlev olmalıdır.

- **validation_function** (function, isteğe bağlı) - Bu işlev, menü öğesinin kullanıcı için kullanılabilir olup olmayacağını belirlemek amacıyla çağrılır. (Gri görünüp görünmeyeceği.) Eğer bir doğrulama işlevi sağlanmazsa, makro her zaman kullanılabilir durumdadır. Bu işlev, [makro doğrulama işlevi API'sini]({{< relref "Registration#macro-validation-function" >}}) takip etmelidir.

- **is_active_function** (function, isteğe bağlı) - Bu işlev, menü öğesinin yanında bir onay işaretiyle gösterilip gösterilmeyeceğini belirlemek için çağrılır. Eğer bir işlev sağlanmazsa, makro hiçbir zaman işaretlenmez. Bu işlev, doğrulama işlevleriyle aynı API'yi kullanır ve aynı uyarıların tümü burada da geçerlidir.

### aegisub.register_filter

Özet: `aegisub.register_filter(name, description, priority, processing_function, configuration_panel_provider)`

Bir dışa aktarma filtresi özelliği kaydeder.

- **name** (string) - Dışa aktarma filtreleri listesinde görüntülenen ad. Ad oldukça kısa olmalıdır.

- **description** (string) - Kullanıcı Dışa Aktar iletişim kutusunda dışa aktarma filtresini vurguladığında açıklama kutusunda görüntülenen açıklama.

- **priority** (number) - Dışa aktarma filtresi uygulamasının başlangıç sırasını belirler. Daha yüksek önceliğe sahip filtreler, daha düşük öncelikli olanlardan daha önce uygulanır. Kullanıcı, Dışa Aktar iletişim kutusunda filtre uygulama sırasını değiştirebilir. Aegisub'ın yerleşik dışa aktarma filtrelerinin öncelikleri:

  - Kare Hızını Dönüştür (Transform Framerate) = 1000 (karaoke efektleri bundan daha yüksek önceliğe sahip olmalıdır)
  - Betik Bilgisini Temizle (Clean Script Info) = 0 (betiğiniz, bunun tarafından temizlenen bilgilere bağlı olabilir)
  - Stilleri Düzelt (Fix Styles) = -5000 (neredeyse her zaman en son çalışmalıdır)

- **processing_function** (function) - Kullanıcı dışa aktarma işlemini başlattığında çağrılan işlev. Bu, [dışa aktarma filtresi işleme işlevi API'sine]({{< relref "Registration#export-filter-processing-function" >}}) sahip bir işlev olmalıdır.

- **configuration_panel_provider** (function, isteğe bağlı) - Dışa aktarma filtresi için bir yapılandırma paneli sağlayan bir işlev. Eğer bu işlev sağlanmazsa, dışa aktarma filtresinin bir yapılandırma paneli olmayacaktır. Bu işlev, [dışa aktarma filtresi yapılandırma paneli sağlayıcısı API'sini]({{< relref "Registration#export-filter-configuration-panel-provider" >}}) takip etmelidir.

## Özellik geri çağırma işlevleri

Bunlar, kayıt işlevlerine sağladığınız geri çağırma işlevleridir.

### Makro işleme işlevi

İmza: `process_macro(subtitles, selected_lines, active_line)`

[`aegisub.register_macro`]({{< relref "Registration#aegisubregister_macro" >}}) işlevine iletilen makro işleme işlevleri bu imzaya sahip olmalıdır. `process_macro` adı, kendi işlev adınız için bir yer tutucudur.

- **subtitles** (user data) - Altyazıları değiştirmek için kullandığınız [altyazı nesnesi]({{< relref "Subtitle_file_interface" >}}).
- **selected_lines** (table) - Seçili satırların indekslerini içeren bir dizi. Bu tablodaki değerler, _subtitles_ nesnesinin başlangıç durumundaki satır indeksleridir. Sadece `dialogue` sınıfındaki satırlar seçilebilir.
- **active_line** (number) - Altyazı düzenleme alanında şu anda düzenleme için kullanılabilir olan satır. Bu, _subtitles_ nesnesine bir indekstir. Bu satır genellikle seçili de olacaktır, ancak bu kesin bir gereklilik değildir.

**Dönüş değeri:**
Makro işleme işlevi iki değere kadar dönüş yapabilir: makro döndükten sonra seçilecek satırların indekslerini içeren yeni bir `selected_lines` tablosu ve yeni `active_line` yapılması gereken satırın indeksi. Eğer ayarlanırsa, yeni aktif satır indeksi, yeni `selected_lines` tablosundaki satırlardan biri olmalıdır.

### Makro doğrulama işlevi

İmza: `validate_macro(subtitles, selected_lines, active_line)`

[`aegisub.register_macro`]({{< relref "Registration#aegisubregister_macro" >}}) işlevine iletilen makro doğrulama işlevleri bu imzaya sahip olmalıdır. `validate_macro` adı, kendi işlev adınız için bir yer tutucudur.

**Önemli, yürütme süresi:** Doğrulama işlevleri her zaman çok hızlı çalışmalıdır. Bu işlevin içinde mümkün olduğunca az işlem yapın, çünkü kullanıcı Otomasyon menüsünü her açtığında bu işlev çalıştırılır ve `validate_macro` içinde harcadığınız her milisaniye, menünün açılmasında bir milisaniyelik gecikme demektir. Kullanıcının çok büyük dosyalar açık tutabileceğini unutmayın. Arayüzü (UI) kilitlemeyin.

- **subtitles** (user data) - Mevcut altyazı dosyası için [altyazı nesnesi]({{< relref "Subtitle_file_interface" >}}). Bu **salt okunurdur**. Doğrulama işlevinde altyazıları değiştiremezsiniz; bunu yapmaya çalışmak çalışma zamanı hatasına neden olur.
- **selected_lines** (table) - Seçili satırların indekslerini içeren bir dizi. Bu tablodaki değerler, _subtitles_ nesnesinin başlangıç durumundaki satır indeksleridir. Sadece `dialogue` sınıfındaki satırlar seçilebilir.
- **active_line** (number) - Altyazı düzenleme alanında şu anda düzenleme için kullanılabilir olan satır. Bu, _subtitles_ nesnesine bir indekstir.

**Dönüş değeri:**
Boolean; eğer makro _subtitles_, _selected_lines_ ve _active_line_ mevcut durumu göz önüne alındığında çalışabiliyorsa `true`, çalışamıyorsa `false`.

Doğrulama işlevi, birincil dönüş değerine ek olarak bir dize (string) döndürebilir. Eğer döndürürse, makronun açıklaması bu dizeye ayarlanır. Bu, kullanıcının makronun neden çalıştırılamayacağına dair bilgilendirilmesi içindir, ancak bunun başka kullanım alanları da olabilir.

### Dışa aktarma filtresi işleme işlevi

İmza: `process_filter(subtitles, settings)`

[`aegisub.register_filter`]({{< relref "Registration#aegisubregister_filter" >}}) işlevine iletilen dışa aktarma filtresi işleme işlevleri bu imzaya sahip olmalıdır. `process_filter` adı, kendi işlev adınız için bir yer tutucudur.

Dışa aktarma filtreleriyle ilgili geri alma (undo) sorunları hakkında endişelenmenize gerek yoktur. Her zaman altyazı dosyasının bir kopyası üzerinde çalışırsınız.

- **subtitles** (user data) - Altyazıları değiştirmek için kullandığınız [altyazı nesnesi]({{< relref "Subtitle_file_interface" >}}). Bu, açık olan altyazı dosyasının bir kopyasıdır, bu nedenle bu altyazı nesnesini değiştirmek açık dosyayı değiştirmez ve sadece dışa aktarılan dosyayı etkiler.
- **settings** (table) - Yapılandırma paneline girilen yapılandırma ayarları veya yapılandırma paneli yoksa boş bir tablo. Bu tablonun biçimi hakkında daha fazla bilgi için [yapılandırma iletişim kutuları]({{< relref "Dialogs" >}}) sayfasına bakın.

**Dönüş değeri:**
Hiçbir şey.

### Dışa aktarma filtresi yapılandırma paneli sağlayıcısı

İmza: `get_filter_configuration_panel(subtitles, old_settings)`

[`aegisub.register_filter`]({{< relref "Registration#aegisubregister_filter" >}}) işlevine iletilen dışa aktarma filtresi yapılandırma paneli sağlayıcıları bu imzaya sahip olmalıdır. `get_filter_configuration_panel` adı, kendi işlev adınız için bir yer tutucudur.

**Önemli, yürütme süresi:**
Bu işlev, kullanıcı Dışa Aktar iletişim kutusunu açtığında otomatik olarak çağrılır ve Aegisub, bir yapılandırma paneliyle dönene kadar bekler. Kullanıcının çok büyük bir dosyası açık olabileceğini ve yapılandırma iletişim kutunuzu oluşturmak için harcanan her milisaniyenin, kullanıcının Dışa Aktar iletişim kutusunun açılmasını beklemesi gereken bir milisaniye daha olduğunu unutmayın. Arayüzü kilitlemeyin.

- **subtitles** (user data) - Mevcut altyazı dosyası için [altyazı nesnesi]({{< relref "Subtitle_file_interface" >}}). Bu **salt okunurdur**. Filtre yapılandırma sağlayıcısında altyazıları değiştiremezsiniz. Altyazıları değiştirmeye çalışmak çalışma zamanı hatasına neden olur.
- **old_settings** (table) - Varsa, yapılandırma paneline daha önce girilmiş olan yapılandırma ayarları. Bir Automation 4 dışa aktarma filtresi çalıştırıldığında, tüm yapılandırma ayarları otomatik olarak orijinal dosyaya kaydedilir. Bu filtre için kayıtlı ayarlar varsa, bunlar varsayılanları doldurmak için bir temel olarak kullanabilmeniz amacıyla _old_settings_ olarak iletilir.

**Dönüş değeri:**
Bir yapılandırma iletişim kutusu tablosu. Bu tablonun biçimi hakkında daha fazla bilgi için [yapılandırma iletişim kutuları]({{< relref "Dialogs" >}}) sayfasına bakın.