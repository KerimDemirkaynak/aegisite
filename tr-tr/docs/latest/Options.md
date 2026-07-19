---
title: Aegisub Seçenekleri
menu:
  docs:
    parent: miscellaneous
weight: 7000
aliases:
  - /docs/latest/Options/
---

Aegisub oldukça özelleştirilebilirdir ve bu nedenle kullanıcı tarafından değiştirilebilir çok sayıda seçeneğe sahiptir. Bu seçeneklere, Görünüm menüsünde bulunan seçenekler iletişim kutusundan erişilebilir. Bu sayfa, mevcut tüm seçeneklerin bir başvuru kılavuzudur.

Aegisub, tüm yapılandırmasını varsayılan olarak [?user]({{< relref "Aegisub_path_specifiers" >}}) dizininde depolanan _config.json_ adlı düz bir metin dosyasında saklar. Aegisub'ı programı yeniden yüklemeden varsayılan seçeneklerine döndürmek isterseniz, config.json dosyasını silebilir ve Aegisub'ı yeniden başlatabilirsiniz.

## Genel

![Genel tercihler](/img/3.2/preferences-general.png#center)

Güncellemeleri Otomatik Denetle
: Etkinleştirilirse, Aegisub periyodik olarak daha yeni bir sürümün mevcut olup olmadığını kontrol eder ve varsa sizi uyarır.
  Doğal olarak, çalışan bir internet bağlantısı gerektirir.

Ana araç çubuğunu göster
: Devre dışı bırakılırsa, Aegisub'ın ana araç çubuğu gizlenir.

Arayüz durumunu altyazı dosyalarına kaydet
: Aegisub, altyazı ızgarasının mevcut kaydırma konumu ve aktif satır numarası gibi bilgileri varsayılan olarak altyazı dosyasında saklar, böylece dosyayı yeniden açtığınızda bu durum otomatik olarak geri yüklenir. Ancak, altyazı dosyalarınız için sürüm kontrolü (source control) kullanıyorsanız, değişikliklerdeki gürültüyü azaltmak için bu özelliği devre dışı bırakmak isteyebilirsiniz.

Araç çubuğu simge boyutu
: Aegisub'daki tüm araç çubuklarında kullanılacak simgelerin boyutu. Şu anda geçerli olan tek değerler 16 ve 24'tür.

Bağlı dosyaları otomatik yükle
: Bir betiği her kaydettiğinizde, Aegisub üzerinde çalışırken açık olan video, ses ve zaman kodu dosyaları hakkında bazı bilgileri betiğin içine kaydeder. Bu seçenek, betiği açarken bu "bağlı" dosyalarla Aegisub'ın ne yapacağına karar verir. "Sor" olarak ayarlanırsa, Aegisub bağlı dosyaları yüklemek isteyip istemediğinizi soracaktır. "Asla" olarak ayarlanırsa, Aegisub bağlı dosyaları asla yüklemeyecektir; aynı şekilde "Her zaman" olarak ayarlanırsa, Aegisub her zaman bağlı dosyaları yüklemeye çalışacaktır (ve dosya(lar) bulunamazsa bir hata raporlayacaktır).

Geri alma seviyeleri
: Geri alınabilecek maksimum değişiklik sayısı. Bu değer ne kadar yüksek olursa, Aegisub o kadar fazla bellek kullanacaktır.

Son Kullanılan Listeler
: Aegisub'daki çeşitli son kullanılan öğe listelerinin her biri için hatırlanacak maksimum öğe sayısı. Bunları artırmanın bellek üzerindeki etkisi önemsizdir, ancak daha uzun listelerin kullanımı zorlaşabilir.

### Varsayılan Stiller

![Varsayılan stiller tercihleri](/img/3.2/preferences-default-styles.png#center)

## Ses

![Ses tercihleri](/img/3.2/preferences-audio.png#center)

Kaydırmayı imleçte kilitle
: Etkinleştirildiğinde, ses dalga formu görünümü, oynatma imleci kenarlara çok yaklaştığında onu takip etmek için otomatik olarak kaydırılır.

Varsayılan olarak işaretçileri kenetle
: Etkinleştirildiğinde, Aegisub, ses işaretçilerini ses ekranındaki diğer işaretçilere (anahtar kareler ve diğer satırların başlangıç veya bitiş zamanları gibi) taşırken, yeterince yakınlarsa tıklama veya sürükleme yoluyla otomatik olarak kenetleyecektir. Kenetleme, shift tuşuna basılı tutularak açılıp kapatılabilir.

Fare tekerleği varsayılan olarak yakınlaştırsın
: Etkinleştirildiğinde, fare tekerleği varsayılan olarak ses ekranını yatay olarak yakınlaştırır ve Ctrl tuşuna basılı tutulduğunda ses ekranını kaydırır. Devre dışı bırakılırsa, bu işlem tersine döner.

Fare üzerine gelindiğinde otomatik odaklan
: Etkinleştirilirse, fare imlecini ses dalga formunun üzerine getirmek, tıklamaya gerek kalmadan otomatik olarak ona odaklanılmasını sağlar.

Video adım adım ilerletilirken sesi oynat
: Etkinleştirilirse, kare atlama işlemi o karenin sesini oynatır.

Varsayılan zamanlama uzunluğu
: Yeni ve zamanlanmamış bir satırın milisaniye cinsinden varsayılan uzunluğu.

Varsayılan giriş süresi uzunluğu
Varsayılan çıkış süresi uzunluğu
: "Giriş süresi ekle" ve "Çıkış süresi ekle" işlevleri tarafından bir satırın başlangıcına ve sonuna eklenen süre. Ayrıca [zamanlama son işleyicisinde]({{< relref "Timing_Post-Processor" >}}) kullanılır (ve buradan ayarlanır).

İşaretçi sürükleme başlangıç hassasiyeti
: Bir işaretçinin sürükleme olarak kaydedilmesi için sürüklenmesi gereken piksel cinsinden mesafe. Daha yüksek değerler, daha az yanıt verebilirlik pahasına kazara yapılan değişiklikleri azaltır.

Sol tıkla sürükleme bitiş işaretçisini taşır
: Etkinleştirildiğinde, sol tıklama satırın başlangıç zamanını tıklanan noktaya ayarlar, ardından satırın bitiş zamanını sürüklenen noktaya ayarlar; bu da tek bir tıkla sürükleme hareketiyle bir satırı zamanlamayı mümkün kılar. Devre dışı bırakıldığında, sol tıkla sürükleme her zaman sadece satırın başlangıç zamanını günceller (sağ tıklamanın bitiş zamanını güncellediği gibi).

Satır sınırı kalınlığı
: Satır başlangıç ve bitiş işaretçilerinin piksel cinsinden genişliği.

Maksimum kenetleme mesafesi
: İşaretçilerin diğer işaretçilere kenetlenmesi için gereken maksimum piksel cinsinden mesafe.

Etkin olmayan satırları göster
: Seçili olan satırı çevreleyen satırların ses dalga formunda nasıl görüntüleneceğini kontrol eder. "Gösterme" sadece mevcut satırı görüntüler. "Öncekini göster" (kronolojik olarak değil, ızgaradaki) bir önceki satırı mevcut satıra ek olarak gri renkte gösterir. "Sonrakini ve öncekini göster" mevcut satırın (kronolojik olarak değil, ızgaradaki) öncesindeki ve sonrasındaki satırları gösterir. "Hepsini göster" mevcut satıra ek olarak tüm satırları gri renkte gösterir.

Yorumlanmış etkin olmayan satırları dahil et
: Devre dışı bırakılırsa, ses ekranında hangi etkin olmayan satırların gösterileceği seçilirken yorum satırları atlanır (bu, "Öncekini göster" seçeneğini "Bu satırdan önceki yorumlanmamış son satırı göster" haline getirir, vb.).

### Görsel Seçenekleri Görüntüle

Anahtar kareler
: Etkinleştirilirse, diyalog zamanlama modundayken (varsayılan) videodaki anahtar karelerin konumlarını işaretleyen çizgiler ses dalga formunda çizilir.

Karaoke anahtar kareleri
: Etkinleştirilirse, karaoke zamanlama modundayken videodaki anahtar karelerin konumlarını işaretleyen çizgiler ses dalga formunda çizilir.

İmleç zamanını çiz
: Etkinleştirilirse, dosyanın başından itibaren geçen süreyi gösteren bir zaman damgası ses dalga formu imlecinin yakınında çizilir.

Video konumu
: Etkinleştirilirse, ses ekranında mevcut video karesinin başlangıç zamanını işaretleyen bir çizgi çizilir.

Dalga formu stili
: Hangi dalga formu oluşturma stillerinin kullanılacağını seçer.

  Maksimum + Ortalama
  : Dalga formu iki tonludur; bir pikselin zaman aralığındaki örneklerin maksimum değerini ve daha parlak bir renkle, zaman aralığındaki tüm örneklerin ortalama değerini gösterir.

  Maksimum
  : Dalga formu, Aegisub'ın önceki sürümlerinde olduğu gibi sadece maksimum değeri görüntüler.

### Ses etiketleri

Bu seçenekler, karaoke heceleri için ses ekranında çizilen etiketlerin görünümünü kontrol eder.

Yazı Tipi
: Ses etiketleri için kullanılacak yazı tipi.

Yazı Boyutu
: Ses etiketleri için kullanılacak yazı tipi boyutu.

## Video

![Video tercihleri](/img/3.2/preferences-video.png#center)

Kaydırıcıda anahtar kareleri göster
: Etkinleştirildiğinde, Aegisub video arama kaydırıcısında anahtar kare işaretçileri çizer.

Seçim değiştiğinde videoyu satır başlangıcına al
: Etkinleştirildiğinde, aktif satır her değiştiğinde Aegisub otomatik olarak videoyu yeni satırın ilk karesine taşır. Bunun, ızgaraya çift tıklayarak veya Ctrl-1 tuşlarına basarak manuel olarak da yapılabileceğini unutmayın.

Görsel araçları her zaman göster
: Devre dışı bırakıldığında, görsel dizgi araçları sadece fare video ekranının üzerindeyken oluşturulur.

Video açıldığında sesi otomatik aç
: Etkinleştirildiğinde, ses verisi de içeren bir video dosyası açtığınızda Aegisub otomatik olarak sesi yükler.

Varsayılan yakınlaştırma
: Varsayılan video yakınlaştırma seviyesi. Çok büyük veya çok küçük bir ekranınız varsa kullanışlıdır.

Kare bazlı hızlı atlama adımı
: Hızlı arama özelliğini (Alt-sağ ok ve Alt-sol ok) kullandığınızda Aegisub'ın ne kadar büyük "sıçramalar" yapacağına karar verir. Kare cinsinden ölçülür.

Ekran görüntüsü kaydetme yolu
: Aegisub'ın ekran görüntülerini nereye kaydedeceğine karar verir. Varsayılan `?video`'dur; bu, ekran görüntülerinin videonun bulunduğu yere kaydedildiği anlamına gelir, ancak bunu istediğiniz herhangi bir yola değiştirebilirsiniz. [Aegisub_yol_belirleyicileri]({{< relref "Aegisub_path_specifiers" >}}) desteklenir; açılır menüde doğrudan bulunan başka bir seçenek de, betiğin bulunduğu yer olan `?script`'tir.

### Betik çözünürlüğü

Açılan ilk videonun çözünürlüğünü kullan
: Etkinleştirildiğinde, bir video açtığınızda ve betik çözünürlüğü henüz ayarlanmamışsa, Aegisub otomatik olarak betik çözünürlüğünü video çözünürlüğüne ayarlar. Devre dışı bırakılırsa, Aegisub bunun yerine betik çözünürlüğünü yapılandırılabilir bir varsayılana ayarlar.

Açılışta video çözünürlüğüyle eşleştir
: Bir video açtığınızda betik çözünürlüğüyle ilgili Aegisub'ın ne yapacağını kontrol eder. "Asla" olarak ayarlanırsa, betik çözünürlüğü video çözünürlüğüyle eşleşmiyorsa Aegisub hiçbir şey yapmaz. "Sor" olarak ayarlanırsa, betik çözünürlüğüyle video çözünürlüğü eşleşmiyorsa, bunları eşleştirmek için betik çözünürlüğünü değiştirmek isteyip istemediğinizi sorar. "Her zaman" olarak ayarlanırsa, Aegisub betiği otomatik olarak video çözünürlüğüyle eşleşecek şekilde her zaman yeniden örnekler.

## Arayüz

![Arayüz tercihleri](/img/3.2/preferences-interface.png#center)

İpucu metinlerini etkinleştir
: Etkinleştirildiğinde, Aegisub bir [geçersiz kılma etiketi]({{< relref "ASS_Tags" >}}) yazdığınızı algılar ve etiketi kapatana kadar söz konusu etiketin sözdizimine dair kısa bir başvuru içeren küçük bir kutu görüntüler. Buna "ipucu metni" (call tip) denir ve bu özellik çeşitli programlama IDE'lerinin kullanıcılarına tanıdık gelebilir.

Zaman kutularında üzerine yaz
: Programdaki tüm zaman düzenleme kutularının davranışını kontrol eder. Varsayılan olarak, Aegisub'daki tüm zaman düzenleme kutuları sanki Insert tuşuna basmışsınız gibi davranır, bu nedenle yazdığınız her rakam zaten orada olanın üzerine yazılır ve orada olan sayıları silemezsiniz; onları üzerine yazmanız gerekir. Bu kutunun işaretini kaldırmak bu davranışı devre dışı bırakır ve zaman düzenleme kutularının normal metin düzenleme kutuları gibi davranmasını sağlar (neredeyse).

Sözdizimi vurgulamayı etkinleştir
: Ana düzenleme kutusundaki geçersiz kılma etiketlerinin sözdizimi vurgulamasını etkinleştirir veya devre dışı bırakır.

Sözlük dosyalarının yolu
: Aegisub'ın yazım denetleyicisi ve eş anlamlılar sözlüğü için sözlük dosyalarını nerede arayacağına karar verir. Varsayılan olarak `?data/dictionaries` içinde arar, ancak doğru biçimdeki kendi sözlükleriniz başka bir yerdeyse, Aegisub'ı oraya yönlendirebilirsiniz.

Yazı Tipi
: Altyazı düzenleme kutusu ve diğer düzenleme kutuları için kullanılan yazı tipini ve boyutunu belirler.

Satır başına maksimum karakter
: Karakter sayacının değeri bu sayıdan yüksekse, maksimum satır uzunluğunu aştığınızı bildirmek için arka plan kırmızıya döner. Maksimum uzunluk başka bir şekilde zorunlu tutulmaz.

Saniye Başına Karakter Uyarı Eşiği
Saniye Başına Karakter Hata Eşiği
: Arka plan CPS sütununun renklendirilmeye başladığı ve hata rengine ulaşıldığı eşikler.

Boşlukları yoksay
: Etkinleştirilirse, boşluklar karakter sayısına dahil edilmez.

Noktalama işaretlerini yoksay
: Etkinleştirilirse, noktalama işaretleri karakter sayısına dahil edilmez.

Tıklandığında ızgaraya odaklan
: Etkinleştirildiğinde, altyazı ızgarası programın kendi alanı gibi davranır ve tıpkı ses veya video gibi odaklanabilir; odaklanmışken etrafında kaydırmak için ok tuşlarını/fare tekerleğini kullanabilirsiniz. Öte yandan, bu seçeneği devre dışı bırakırsanız, ızgaraya her tıkladığınızda odak, tıklandığı yerde kalır. Bu, ızgarada artık klavye kısayollarını kullanamayacağınız anlamına gelir, ancak ses odağını kaybetmeden bir satıra gitmek için ızgaraya tıklayabileceğiniz anlamına gelir. Kendi takdirinize göre kullanın.

Görünür altyazıları vurgula
: Etkinleştirildiğinde, video karesinde o an görünür olan (veya en azından görünür olması gereken; Aegisub bu durumda alfa ve benzeri hileleri hesaba katmaz; sadece satırın zamanlamasıyla ilgilenir) tüm altyazı satırları ızgarada özel bir arka plan rengiyle vurgulanır (aşağıdaki "Kare içindeki satır arka planı" seçeneğine bakın).

Geçersiz kılma sembolünü gizle
: Etiket gizleme aktifse geçersiz kılma blokları yerine gösterilecek karakter. Adına rağmen, dilerseniz bunun birden fazla karakter olabileceğini unutmayın.

Yazı Tipi
: Izgaradaki tüm metinlerin yazı tipini ve boyutunu belirler.

### Renkler

![Renk tercihleri](/img/3.2/preferences-colours.png#center)

#### Ses Ekranı

Oynatma imleci
: Oynatma imlecinin rengi.

Satır sınırı başlangıcı
Satır sınırı bitişi
Satır sınırı etkin olmayan satır
: Çeşitli satır sınırı işaretçilerinin ilgili renkleri.

Hece sınırı
: Karaoke modundaki bir hece sınırı çizgisinin rengi.

### Renk Şemaları

Dalga formu/spektrum ve bazı arayüz öğeleri için kullanılan renk şemasını kontrol eder. Aegisub'ın şu anda renk şemalarını düzenlemek veya yenilerini oluşturmak için bir arayüzü yoktur, ancak maceracı hissediyorsanız bunlara config.json dosyasından ulaşabilirsiniz.

#### Sözdizimi Vurgulama

Normal
: Normal metnin rengi.

Parantezler
: Geçersiz kılma bloklarını başlatan/bitiren parantezlerin rengi.

Eğik çizgiler ve parantezler
: Geçersiz kılma bloklarındaki ters eğik çizgilerin ve parantezlerin rengi.

Etiketler
: Geçersiz kılma bloklarındaki etiket isimlerinin rengi.

Parametreler
: Geçersiz kılma etiketlerine ait parametrelerin rengi.

Hata
: Geçersiz kılma bloğu içindeki geçersiz sözdizimi için hata rengi.

Hata arka planı
: Hatalar için arka plan rengi.

Satır sonu
: Geçersiz kılma blokları dışındaki \\N, \\n ve \\h için renk.

Karaoke şablonları
: Şablon satırlarındaki karaoke şablonlayıcı blokları için renk.

#### Altyazı Izgarası

Standart ön plan
Standart arka plan
: Izgaradaki satırların normal rengi. "Ön plan" metin rengidir, "Arka plan" ise arka plan rengidir.

Seçim ön planı
Seçim arka planı
: Izgarada seçili satırların rengi.

Yorum arka planı
Seçili yorum arka planı
: Yorumlanmış satırların ve seçili yorumlanmış satırların arka plan rengi.

Çakışma ön planı
: Zamanlaması o an aktif olan satırla çakışan satırların metin rengi.

Kare içindeki satır arka planı
: Video karesinde o an görünür olan satırların arka plan rengi.

Başlık
Sol sütun
Aktif satır kenarlığı
Satırlar
: Izgara çizgilerinin ve sabit sütunların/başlıkların rengi.

## Kısayol Tuşları

![Kısayol tuşu tercihleri](/img/3.2/preferences-hotkeys.png#center)

Bu sayfa Aegisub'da o an ayarlı olan tüm kısayol tuşlarını listeler ve bunları eklemenize, kaldırmanıza veya değiştirmenize olanak tanır.

### Kısayol Tuşu Bağlamları

Aegisub, programın hangi kısmının odağa sahip olduğuna bağlı olarak farklı kısayol tuşları ayarlamayı destekler.

"Varsayılan" grubu, Aegisub'da o an hangi öğenin klavye odağına sahip olduğuna bakılmaksızın çalışması gereken kısayol tuşları içindir. Varsayılan grupta ayarlanan kısayol tuşları, geçerli olduğunda daha özel kategoriler tarafından geçersiz kılınır.

"Her zaman" grubu, programın her yerinde uygulanan ve düzenleme kutularındaki normal yazma dahil olmak üzere diğer tüm tuş vuruşlarını geçersiz kılan, Medusa modu tarafından etkinleştirilen kısayol tuşlarını ayarlar.

Diğer tüm kısayol tuşu bağlamları kendi kendini açıklamalıdır.

### Kısayol tuşlarını ayarlama

Bir kısayol tuşunu değiştirmek için önce satıra tıklayarak onu seçin, ardından satırdaki kısayol tuşu alanına tıklayın ve ardından komutu tetiklemesi gereken tuş(lar)a basın. Yeni kısayol tuşunu başka bir satıra tıklayarak kabul edin.

Yeni bir kısayol tuşu eklemek için kısayol tuşunu eklemek istediğiniz bağlamı seçin, ardından Yeni düğmesine tıklayın. [Komut adını]({{< relref "Commands" >}}) girin, ardından düzenleme yaparken olduğu gibi kısayol tuşunu ayarlayın.

## Yedekleme

![Yedekleme tercihleri](/img/3.2/preferences-backup.png#center)

### Otomatik Kaydet

Etkinleştir
: Etkinleştirilirse, Aegisub üzerinde çalıştığınız betiğin bir kopyasını periyodik olarak otomatik kaydetme yoluna kaydeder.

Saniye cinsinden aralık
: Aegisub'ın ne sıklıkla otomatik kaydedeceği.

Yol
: Üzerinde çalıştığınız betiklerin otomatik kaydedilen kopyalarının nereye kaydedileceğine karar verir. Varsayılan olarak Aegisub `?user` dizininizdeki `autosave` klasörüne ayarlanmıştır (ayrıntılar için [Aegisub_yol_belirleyicileri]({{< relref "Aegisub_path_specifiers" >}}) sayfasına bakın).

Her değişiklikten sonra otomatik kaydet
: Etkinleştirilirse, Aegisub dosyayı üzerinde yapılan her değişiklikten sonra kaydeder. Bunun şu anda geri alma sistemiyle ilgili bazı sorunlara neden olduğunu unutmayın.

### Otomatik Yedekleme

Etkinleştir
: Etkinleştirilirse, Aegisub açtığınız her betiğin bir yedek kopyasını, açar açmaz kaydeder. Varsayılan olarak, `?user/autoback/` dizinine kaydedilir, ancak bu değiştirilebilir (aşağıya bakın).

Yol
: Betiklerin otomatik yedek kopyalarının nereye kaydedileceğine karar verir. Varsayılan olarak Aegisub `?user` dizininizdeki `autoback` klasörüne ayarlanmıştır.

## Otomasyon

![Otomasyon tercihleri](/img/3.2/preferences-automation.png#center)

Temel yol
: Otomatik yüklenmeyen otomasyon betiklerini koyduğunuz temel dizin. Sadece altyazı dosyalarındaki betik dosyalarına giden yolları kaydetmek için kullanılır.

Dahil etme yolu
: Dahil etme dosyalarının ve modüllerin arandığı dizinlerin listesi. Dizinler, `|` karakteri ile ayrılır.

Otomatik yükleme yolu
: Başlangıçta betiklerin arandığı ve ardından otomatik olarak yüklenen dizinlerin listesi. Dizinler, `|` karakteri ile ayrılır.

İzleme seviyesi
: Bir betik hata ayıklama konsoluna bir mesaj gönderdiğinde, bir izleme seviyesi de belirleyebilir. Bir mesajın izleme seviyesi burada verilen değerden düşükse, mesaj günlüğe kaydedilmez. Seviyelere verilen isimler sadece öneridir ve betiğin yürütülmesi üzerinde herhangi bir etkileri yoktur. (yani, "Kritik" seviyesinde bir mesaj betiğin sonlanmasına neden olmaz.)

Dışa Aktarırken Otomatik Yeniden Yükle
: [Dışa Aktarma]({{< relref "Exporting" >}}) iletişim kutusu açıldığında, belirtilen betik setlerini otomatik olarak yeniden yükler. Bu durumda, [Otomasyon/Yönetici]({{< relref "Automation/Manager" >}}) penceresine girmeniz ve hatanın nedenini belirlemeniz gerekecektir.

## Gelişmiş Ses

![Gelişmiş ses tercihleri](/img/3.2/preferences-advanced-audio.png#center)

Ses sağlayıcı
: Sesi yüklemek için hangi arka ucun kullanılacağı. Şu anda sadece iki yöntem mevcuttur.

  _avisynth_ (Sadece Windows)
  : Sesi yüklemek için [Avisynth](https://avisynth.nl/index.php/Main_Page) kullanır. AVS dosyalarının Import() ile açılması dışında tüm dosya türleri DirectShowSource() ile yüklenecektir.

  _FFmpegSource_
  : Sesi yüklemek için [FFMS2](https://github.com/FFMS/ffms2) kullanır. Genellikle DirectShowSource üzerinden açmaktan daha güvenilirdir, ancak dosyaları önce indekslemesi gerektiğinden daha yavaştır.

  Bu ayardan bağımsız olarak, WAV dosyaları için her zaman dahili PCM WAV okuyucusu denenir.

Ses oynatıcı
: Ses oynatmak için hangi yöntemin kullanılacağı. Seçenekler platforma bağlıdır.

  _DirectSound_ (Sadece Windows)
  : Sesi oynatmak için Microsoft DirectSound kullanır. En iyi test edilmiş ve en kararlı ses oynatıcıdır.

  _DirectSound-old_ (Sadece Windows)
  : Aegisub'ın orijinal DirectSound oynatıcı uygulamasıdır. DirectSound oynatıcıyı kullanırken ses oynatma sorunları yaşıyorsanız, bu daha iyi çalışabilir (ama muhtemelen çalışmayacaktır).

  _alsa_ (Sadece Linux)
  : Sesi oynatmak için [Advanced Linux Sound Architecture](https://www.alsa-project.org/) kullanır. ALSA, Linux'un yerel ses mimarisidir ve başka hiçbir sistemde mevcut değildir.

  _pulse_ (Linux ve diğer *NIX benzeri sistemler)
  : Sesi bir [PulseAudio](https://pulseaudio.org/) ses sunucusu aracılığıyla oynatır. Ses oynatıcılar arasında en az test edilmiş ve çalışma olasılığı en düşük olanıdır; sadece ses kurulumunuz pulse olmayan oynatıcıları istenmeyen kılıyorsa önerilir.

  _portaudio_
  : Sesi oynatmak için [PortAudio](https://www.portaudio.com/) API'sini kullanır. PortAudio'nun farklı platformlarda farklı oynatma uygulamaları vardır. Çoğu Unix sisteminde çıkış için Open Sound System (OSS) kullanır. Şu anda çıkış cihazı seçimini destekleyen tek Windows ses oynatıcısıdır.

  _openal_
  : Sesi oynatmak için [OpenAL](https://www.openal.com/) API'sini kullanır. OS X'te önerilen oynatıcıdır. Windows sürümlerinde genellikle bulunmaz çünkü çok az yarar sağlarken fazladan bir bağımlılık ekler.

### Önbellek

Önbellek türü
: Çok az RAM'iniz yoksa RAM kullanın, varsa Sabit Disk kullanın. PCM WAV dosyaları açıldığında önbelleğe gerek yoktur ve kullanılmaz. Önbelleği devre dışı bırakırsanız, ses oynatma çok güvenilmez hale gelebilir.

Yol
Dosya adı
: Bu seçenekler, sabit disk ses önbelleğinin nerede bulunacağını belirler. Sadece önbellek sabit disk olarak ayarlandığında kullanılır. Disk alanınız az olmadıkça bunu değiştirmeniz gerekmemelidir. İsim için, dize printf tarzında "%i" parametresi bekler; bu, bir sayı ile değiştirilecektir. Varsayılan olarak "%02i" kullanılır. Ne yaptığınızı bilmiyorsanız bunu değiştirmeyin.

### Spektrum

Spektrum kalitesi
: Ses spektrumu ekranının kalitesini belirler. Daha yüksek kalite ayarları daha büyük CPU ve RAM kullanımına neden olur. Her ardışık ayar bir öncekinden biraz daha fazla CPU ve iki kat daha fazla RAM kullanır. 48 kHz örnekleme hızındaki ses için, bir dakikalık ses farklı ayarlarda bu kadar bellek kullanır:

  <table class="table table-bordered table-condensed">
      <tr><th>0 "normal"</th><td>11 MB</td>
      <tr><th>1 "daha iyi"</th><td>22 MB</td>
      <tr><th>2 "yüksek"</th><td>44 MB</td>
      <tr><th>3 "çılgın"</th><td>88 MB</td>
    </table>

  Kullanılan bellek miktarı kanal sayısına (Aegisub her zaman mono çalışır) veya sesin bit derinliğine (spektrum her zaman 32 bit kayan noktalı olarak hesaplanır) bağlı değildir.

{{<todo>}}bu muhtemelen yanlış{{</todo>}}

Önbellek bellek maksimumu
: Ses spektrumu önbelleğe alma için kullanılacak maksimum bellek miktarı. Ses spektrumunu görüntülemek için yapılan hesaplamaların sonuçları, seste gezinmeyi daha akıcı hale getirmek için önbelleğe alınır. Bir miktar bellekte önbelleğe alınabilecek spektrum ekranı miktarı, yukarıdaki kalite ayarına bağlıdır. Varsayılan 128 MB'lık önbellek boyutu, 1. kalite ayarında 48 kHz'de 6 dakikadan biraz daha az ses sağlar. Bunu 5 MB'tan daha küçük ayarlarsanız, bunun yerine varsayılan 128 MB kullanılır. Bunu muhtemelen kurulu fiziksel RAM miktarınızın 1/4'ünden fazla ayarlamamalısınız.

### Avisynth (Sadece Windows)

Avisynth aşağı-karıştırıcı
: Aegisub sadece mono (tek kanallı) ses kullanabilir. Bu seçenek, sesi mono'ya dönüştürmek için hangi Avisynth işlevinin kullanılacağını belirler.

Örnekleme hızını zorla
: Açılan tüm sesi verilen örnekleme hızına dönüştürür. Örnekleme hızını ses kartınızın kullandığı hızda zorlamak (ses oynatıcısının yapması yerine), ses performansını potansiyel olarak artırabilir ve oynatma sorunlarını çözebilir.

### FFmpegSource

Ses indeksleme hata işleme modu
: Bir ses parçasını indekslerken bir hata oluşursa ne yapılacağı.

  _Yoksay_
  : Hatayı yoksay ve dosyanın kodunu çözmeye devam et. Bu mod bazı bozuk dosyaları açmanıza izin verebilir, ancak ses/video senkronizasyonunun kaymasına neden olabilir.

  _Temizle_
  : Dosyada hata içeren parçanın mevcut olmadığını varsay.

  _Durdur_ (varsayılan)
  : İndekslemeyi hatanın olduğu noktada durdur ve hatadan önceki tüm ses verilerini döndür. Dosyaların en sonundaki bozuk ses paketleri oldukça yaygın olduğundan varsayılan budur.

  _İptal et_
  : Dosyayı açmayı tamamen reddet.

Tüm ses parçalarını her zaman indeksle
: Devre dışı bırakılırsa, bir video dosyası açmak sadece video parçalarını indeksleyecektir, bu da aynı dosyadan ses parçalarını açmak için dosyayı yeniden indekslemenizi zorunlu kılar.

### Portaudio

Portaudio cihazı
: Portaudio aracılığıyla ses oynatırken hangi çıkış cihazının kullanılacağı.

## Gelişmiş Video

![Gelişmiş video tercihleri](/img/3.2/preferences-advanced-video.png#center)

Video sağlayıcı
: Aegisub'ın videoyu yüklemek için hangi yöntemi kullanacağına karar verir. Burada hangi seçeneklerin mevcut olduğu, Aegisub kopyanızın nasıl derlendiğine ve hangi işletim sisteminde çalıştığınıza bağlıdır. Aşağıdaki alternatifler mevcuttur:

  _avisynth_ (Sadece Windows)
  : Videoyu yüklemek için [Avisynth](https://avisynth.nl/index.php/Main_Page) kullanır. Çok yönlüdür, doğru eklenti sağlanırsa neredeyse tüm yaygın formatları ve .d2v dosyalarını (indekslenmiş DVD VOB'ları) yüklemeyi destekler. Aegisub'ın istenirse sistem kurulumunuzu kullanmak yerine kendi avisynth.dll dosyasını yükleyebileceğini unutmayın. En iyi performans için AVI dosyaları için Video for Windows kod çözücüleri gerektirir. Çoğu format için DirectShow kullanır, bu nedenle AVI, d2v ve Avisynth betikleri açmak dışında herhangi bir şey için önerilmez.

  _FFmpegSource_
  : Videoyu yüklemek için [FFMS2](https://github.com/FFMS/ffms2) kullanır. Genellikle en güvenilir seçenektir.

Altyazı sağlayıcı
: Aegisub'ın videodaki altyazıları oluşturmak için hangi arka ucu kullanacağına karar verir.
  VSFilterMod veya xy-VSFilter gibi ek CSRI oluşturucuları yüklerseniz (dll'leri Aegisub dizinindeki CSRI dizinine yerleştirerek), bunlar varsayılanlarla birlikte burada listelenecektir.

  *CSRI/vsfilter_textsub* (Sadece Windows)
  : Altyazıları oluşturmak için VSFilter 2.40 kullanın. Bu, Aegisub tarafından kullanılan ASS biçimini tanımlayan standart altyazı oluşturucusudur.

  _libass_
  : Altyazıları oluşturmak için [libass](https://github.com/libass/libass) kullanın. libass, VSFilter'dan çok daha hızlıdır ve (bir nebze) çapraz platformdur, ancak ne yazık ki hala VSFilter'dan bazı oluşturma farklılıkları ve Windows'ta yazı tipi ile ilgili sorunları vardır. [Yumuşak altyazılı]({{< relref "Attaching_subtitles_to_video#softsubbing" >}}) karmaşık dizgi çalışmaları yapıyorsanız, işinizi hem VSFilter hem de libass ile kontrol etmek iyi bir fikirdir, çünkü gittikçe daha fazla kullanıcı libass kullanmaktadır.

BT.601'i zorla
: VSFilter uyumluluğu için tüm YUV videolarını BT.601 gibi varsayın.

  VSFilter, DirectShow filtresi olarak kullanıldığında, altyazıları RGB'den YUV'ye dönüştürmek için her zaman BT.601 renk matrisini kullanır. Bu, videonun BT.709 kullanması durumunda (çoğu HD videoda ve bazı DVD'lerde olduğu gibi), Aegisub'daki videoyla eşleşen renklerin oynatıcıdaki videoyla eşleşmeyeceği anlamına gelir. Bu seçenek, Aegisub'ın videoları her zaman BT.601 kullanarak RGB'ye dönüştürmesini sağlar; bu, Aegisub'da gösterilen renkleri yanlış kılar ancak renkler Aegisub'da eşleşirse oynatıcıda da eşleşecekleri şekilde ayarlar.

  İşleri daha heyecanlı hale getirmek için, VSFilter MPC-HC'de dahili altyazı oluşturucusu olarak kullanıldığında *doğru* renk uzayını kullanır, bu nedenle bu seçeneği etkinleştirmek bu durumda renklerin *uyumsuz* olmasına neden olur. ISR (dahili oluşturucu) şu anda birçok yönden bozuk olduğundan (örneğin, altyazıları onunla doğru bir şekilde konumlandırmak imkansızdır), şimdilik bu konuda endişelenmemenizi öneririz.

  Bu karşılaştırma durumu daha netleştirebilir:

  ![bt601](/img/3.2/bt601.png)

  Aegisub artık RGB -> YUV dönüşümleri için hangi renk uzayının kullanılması gerektiğini altyazı dosyasına yazıyor, bu yüzden umarız bu karmaşa gelecekte oluşturucu iyileştirmeleriyle çözülecektir.

### Avisynth

2.56a öncesi Avisynth'e izin ver
: Bazı insanların çeşitli kötü nedenlerden dolayı yükseltmeyi reddettiği eski Avisynth sürümlerini kullanmayı destekleyin.

Avisynth bellek sınırı
: Avisynth için kare önbelleği bellek sınırı. Bunu artırmak genellikle performansı artırmaz ve sadece doğrudan aşırı karmaşık Avisynth betikleri açıyorsanız yapılmalıdır.

### FFmpegSource

Hata ayıklama günlüğü ayrıntısı
: ffmpeg/libav'ın ayrıntı düzeyini ayarlayın. Sadece Aegisub'a eklenmiş bir hata ayıklayıcınız olduğunda etkilidir.

Kod çözme iş parçacıkları
: Videonun kodunu çözmek için kullanılacak maksimum iş parçacığı sayısı veya otomatik seçim için -1. Bunu 1'e ayarlamak, performans pahasına bazı kod çözme sorunlarını düzeltebilir. 1 veya -1 dışında bir değere ayarlamak için nadiren bir neden vardır.

Güvensiz aramayı etkinleştir
: Videoda arama yaparken FFMS2'nin bazı doğruluk kontrollerini devre dışı bırakın. FFMS2'nin kare bazında doğru arama yapamadığı bazı dosyaları açmayı mümkün kılar.