---
title: Stilleri düzenleme
menu:
  docs:
    parent: typesetting
weight: 4200
aliases:
  - /docs/latest/Styles/
---

ASS formatındaki bir **stil**, diyalog satırlarına uygulanan tipografik biçimlendirme kuralları kümesidir. Stil parametreleri [geçersiz kılma etiketleri]({{< relref "ASS_Tags" >}}) ile değiştirilebilir; stiller, her satır için tüm geçersiz kılma kodlarını yazmak zorunda kalmamanız için vardır.

## Stil yöneticisi

Aegisub'ın stil yöneticisi aracı (Altyazılar menüsünden erişilir), stilleri düzenlemek, kaydetmek ve düzenlemek için çeşitli yollar sunar. Şu şekilde görünür:

![Stil_yöneticisi](/img/3.2/Style_manager.png#center)

Gördüğünüz gibi pencere ikiye bölünmüştür. Sağ taraf, şu anda yüklenmiş olan betiğinizde erişilebilir olan tüm stilleri görüntüler; sol taraf ise bir stil deposunu temsil eder. Stil depoları, Aegisub tarafından stilleri kaydetmeniz ve bunları betiklere hızlıca aktarmanız için kullanılır. İstediğiniz kadar depo oluşturabilirsiniz; bazı insanlar tüm stillerini tek bir depoda tutmayı tercih ederken, diğerleri stillerini yazı tipine, gösterime veya alfabetik sıraya göre ayırır. Üst kısımdaki açılır menü, hangi depoyu görüntülemek istediğinizi seçmenizi sağlar.

Pencerenin alt kısmında, biri depo, diğeri geçerli betik için olmak üzere birbirinin neredeyse aynısı iki dizi düğme bulunur. Bunlar:

Yeni
: Depoda veya geçerli betikte yeni bir stil oluşturun.

Düzenle
: Seçili stili stil düzenleyiciyi kullanarak düzenleyin (aşağıya bakın).

Kopyala
: Seçili stilin bir kopyasını oluşturun ve düzenlemek için stil düzenleyiciyi açın.

Sil
: Seçili stili/stilleri silin.

Betiğe kopyala ve Depoya kopyala
: Seçili stilleri depo ile geçerli betik arasında kopyalar.

Beti̇kten i̇çe aktar
: Bir veya daha fazla stili başka bir betikten geçerli olana aktarın.

Stil yöneticisinde Ctrl-C tuşlarına basmak, seçili stili/stilleri metin dizisi olarak panoya kopyalar. Bu işlem tersi için de çalışır; başka bir programdan bir veya daha fazla stil satırını kopyalayıp stil yöneticisinde Ctrl-V (yapıştır) tuşlarına basarsanız, bunlar geçerli betiğe eklenir.

## Stil düzenleyici

"Düzenle" düğmesine basmak veya bir stil adına çift tıklamak, mevcut tüm parametreleri ayarlamanıza olanak tanıyan stil düzenleyiciyi açar. **Not**: Geçersiz kılma etiketi olarak mevcut olan bazı parametreler (örneğin `\be`) stil parametresi olarak _mevcut değildir_; tersine, stil düzenleyicide mevcut olan bazı parametreler (örneğin "opak kutu" kenarlık seçeneği) stil geçersiz kılma olarak _mevcut değildir_. Bu, biçimsel bir kısıtlamadır ve bazen can sıkıcı olabilir.

Stil düzenleyiciye dönmek için:

![Stil_düzenleyi̇ci̇](/img/3.2/Style_editor.png#center)

Stil adı
: Stil adı. Aynı betikte aynı isme sahip iki stil olamaz.

Yazı tipi
: Bu bölüm yazı tipi ayarlarını kontrol eder. Açılır menü yazı tipini seçmenizi sağlar (sisteminizde yüklü olan tüm yazı tipleri bu listede görünecektir) ve sağdaki sayı boyutu punto cinsinden kontrol eder. Aşağıdaki onay kutuları kalın/italik/altı çizili/üstü çizili parametrelerini ayarlar.

Renkler
: Bu, dört metin rengini (birincil, ikincil, kenarlık ve gölge) kontrol eder. Her birinin anlamı şu şekildedir:

  **Birincil:**
  Metin gövdesinin ana "dolgu" rengi.

  **İkincil:**
  Karaoke efektleri için kullanılan ikincil dolgu rengi (bkz: `\k` ve ilişkili etiketler, [geçersiz kılma etiketleri sayfası]({{< relref "ASS_Tags#karaokeeffect" >}})).

  **Kenarlık (Outline):**
  Metnin kenar rengi.

  **Gölge (Shadow)**
  Ana metnin altında görüntülenen ve sağ tarafta tanımlanan gölge genişliğine göre kaydırılan gölge rengi.

  Dört renkli kutu, dört metin renginin her biri için mevcut rengi gösterir; üzerlerine tıklamak [renk seçiciyi]({{< relref "Colour_Picker" >}}) açar.

Kenar boşlukları
: Metnin video çerçevesinin kenarlarına ne kadar yakın konumlandırılacağını kontrol eder (dolayısıyla otomatik satır kırılmasının ne zaman devreye gireceğini de belirler; ancak metin yaslama seçeneği olmadığını unutmayın). Her değer (sol, sağ, dikey) betik çözünürlüğü pikseli cinsinden verilir (bkz: [betik özellikleri]({{< relref "Properties" >}})). Hizalamalar (`\an`) 1-3 için dikey kenar boşluğu, video çerçevesinin altına göredir; 4-6 için herhangi bir anlamı yoktur ve 7-9 için video çerçevesinin üst kısmına göredir.

Hizalama
: Metnin hizalamasını kontrol eder. Sayılar `\an` etiketinin bağımsız değişkenlerine karşılık gelir. 1, 4 ve 7 sola yaslıdır; 3, 6 ve 9 sağa yaslıdır; 2, 5 ve 8 ortalıdır. 1, 2 ve 3 "altyazı"dır (yani çerçevenin altına çizilir); 4, 5 ve 6 "orta başlık"tır (yani çerçeve üzerinde dikey olarak girilir); 7, 8 ve 9 "üst başlık"tır (yani çerçevenin üstüne çizilir). İki yana yaslı hizalama diye bir şey olmadığını unutmayın; bu bir biçim kısıtlamasıdır.

Kenarlık (Outline)
: Kenarlık (sınır) kalınlığını (ve stilini) ve gölge ofsetini kontrol eder.

  - Kenarlık için, ScaledBorderAndShadow (ÖlçekliKenarlıkVeGölge) etkinleştirilmişse sayı, betik pikseli cinsinden kenarlık kalınlığıdır (bkz: [betik özellikleri]({{< relref "Properties" >}})); devre dışı bırakılmışsa kalınlık video pikseli cinsinden verilir. 0 olarak ayarlanması kenarlığı devre dışı bırakır.
  - Öte yandan gölge, ana metnin bir kopyasıdır ve belirtilen miktarda aşağı ve sağa kaydırılır. ScaledBorderAndShadow etkinse mesafe betik pikseli, değilse video pikseli cinsindendir. 0 olarak ayarlanması gölgeyi devre dışı bırakır.
  - Son olarak, "Opak kutu" olarak işaretlenmiş onay kutusu, kenarlığın yukarıda açıklandığı gibi çizilip çizilmeyeceğini (işaretlenmediğinde gerçekleşir) veya opak bir arka plan sınırlayıcı kutusu ile değiştirilip değiştirilmeyeceğini kontrol eder. Opak kutu kenarlıklarının oluşturulmasının, yazı tipi ölçeği %100'den farklı olduğunda bozuk olduğunu unutmayın.

Çeşitli
: Bu bölüm başka çeşitli parametrelere sahiptir, yani:

  Ölçek X/Y
  : Metin uzamasını sırasıyla yatay (X) ve dikey (Y) yönde kontrol eder. Değer yüzde olarak verilir, yani 100 hiçbir uzama yapılmadığı anlamına gelir. Bunu normal metin boyutlandırma için kullanmamalısınız; bunun yerine Yazı Tipi alanındaki punto değerini kullanın çünkü bu, yazı tipinden gelen ipucu bilgilerini kullanır.

  Döndürme
  : Metnin döndürülmesini kontrol eder. Değer, derece cinsinden dönüş açısıdır (tam bir daire için 360 derece) ve negatif veya 360'tan büyük olabilir (360, 720 vb. olarak ayarlamak, [animasyonlu dönüşümler]({{< relref "ASS_Tags#animatedtransform" >}}) söz konusu olmadıkça 0 olarak ayarlamakla aynıdır).

  Aralık:
  : Harfler arasındaki yatay boşluğu kontrol eder. 0, yazı tipi varsayılanlarının kullanıldığı anlamına gelir. Daha az boşluk için negatif veya daha fazla boşluk için pozitif olabilir. Değer, her karakter arasındaki piksel cinsinden ek boşluktur; bunların betik pikseli mi yoksa video pikseli mi olduğu tam olarak tanımlanmamıştır.

  Kodlama:
  : Yazı tipi seçimini, yalnızca belirlenen eski Windows kod sayfasını desteklediğini bildiren yazı tipleriyle sınırlandırır. Tüm geçerli değerler Microsoft tarafından [bu sayfada](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-wmf/0d0b32ac-a836-4bd2-a112-b6000a1b4fc9) listelenmiştir.
    Eğer `1` (varsayılan karakter kümesi) olarak ayarlanırsa, yazı tipi seçimi sınırsızdır.<br/>
    Bu bir zamanlar geçmişte yararlı olmuş olabilir, ancak bugün bunu `1` dışında bir değere ayarlamamalısınız.
    İstediğiniz yazı tiplerini seçmek için doğru ve benzersiz adlarını belirtin.
    Ayrıca, libass (0.17.1 itibarıyla) Kodlama alanını tam olarak desteklemediğinden, yazarlık sırasında `1` dışındaki değerler için elde ettiğiniz sonuç, izleyicilerin oynatma sırasında gördüğünden farklı olabilir.<br/>
    Bunun gerçek metnin kodlamasıyla hiçbir ilgisi yoktur.

  Önizleme:
  : Mevcut stil parametreleri kullanılarak metnin nasıl görüneceğinin bir önizlemesini gösterir. Metin alanı, önizleme için bazı örnek metinler girmenize olanak tanır ve renkli kutu arka planın rengini kontrol eder.